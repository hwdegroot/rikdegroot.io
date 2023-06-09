---
title: How to run and deploy gitlab pages on your own domain
type: post
tags:
    - development
    - gitlab
    - google domains
    - let's encrypt
    - lang-en
date: 2019-07-18T21:50:57Z
images:
    - images/og/gitlab+letsencrypt.png
showComments: true

---

Not so long ago I had to make a static website, and was figuring out how to do this. I came across [hugo](https://gohugo.io). And I
really liked how quickly you can build and publish a website from markdown.

A while ago google made the [.dev](https://domains.google/#/) available for peanuts, so, impulsively, I bought one.
From $12 you can get one, and start doing awesome stuff with this. But I didn't. I parked the domain for a while.
There are plenty of cloud providers that will host your website for you, like [AWS](https://aws.amazon.com/), [Netlify](https://www.netlify.com) and many more.

But I had no clue where to host this, because I am lazy and cheap. Then for work I had to do something similar, and I wondered if I could just host
my [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/) on my own domain. And guess what, you can, and it is amazingly simple!

I started to write out some boilerplate (easy), picked a theme I liked (easy, I used [m10c](https://themes.gohugo.io/hugo-theme-m10c/)), and off I went.

Here I will try to explain how I got from writing some basic _markdown_ to running it on my own domain
(well, technically it doesn't. But it appears so).

You can find the repository of this site [here](https://gitlab.com/hwdegroot/forsure.dev). I like `yaml` over `toml`.
Therefor I will use the `yaml` configuration option from hugo.

My config is as follows, but also available [here](https://gitlab.com/hwdegroot/forsure.dev/blob/main/site/config/config.yaml)

```yaml
title: Rik de Groot
baseURL: https://www.forsure.dev/
enableRobotsTXT: true
languageCode: en-us
assetsDir: content/assets
themesDir: themes
metaDataFormat: yaml
permalinks:
    posts: /-/:year/:month/:day/:title
    tags: /:slug
paginate: 10
theme: m10c
enableGitInfo: true
googleAnalytics: <GA tracking code>

# enable auto code highlighting without effort
pygmentsCodefencesGuessSyntax: true
pygmentsUseClasses: true
pygmentsStyle: monokai
pygmentsCodeFences: true

# Site parameters
params:
    author: Rik de Groot
    description: Code, cook and bake. Tech Lead @FinLeaseNL
    avatar: assets/images/rik-de-groot.jpg
    images:
        - assets/og/cover.png
    social:
        - name: gitlab
          url: https://gitlab.com/hwdegroot
        - name: twitter
          url: https://twitter.com/hwdegroot
        - name: linkedin
          url: https://www.linkedin.com/in/rikhwdegroot/
    ## Use the green styles
    style:
        darkestColor: "#282e37"
        darkColor: "#3d434c"
        primaryColor: "#67eba2"
        lightColor: "#d3d3d3"
        lighestColor: "#fff"

```

The nice thing about using the tools that are popular, is that a lot of people already figured out stuff for you. All you need to do is Google it.
So I did. You can find all about deploying a hugo app to GitLab pages in [this example](https://gitlab.com/pages/hugo).

I used the following `.gitlab-ci.yml` configuration to get the job done. Gitlab published a [docker container](https://registry.gitlab.com/pages/hugo:latest),
that can be used to build your project (see the above example form GitLab). But I like to have the extended features as well, so [I created my own](https://gitlab.com/hwdegroot/forsure.dev/blob/main/Dockerfile) which is available in the [container registry of the project](https://gitlab.com/hwdegroot/forsure.dev/container_registry). But not too much credits to myself, because I based it on the container from [jguyomard](https://github.com/jguyomard).
You can find the project on [GitHub](https://github.com/jguyomard/docker-hugo).


```yaml
# .gitlab-ci.yml
stages:
    - pages

# the theme is submoduled, so make sure to do a recursive clone
variables:
    GIT_SUBMODULE_STRATEGY: recursive

pages:
    stage: pages
    image: registry.gitlab.com/hwdegroot/forsure.dev/hugo:latest
    before_script:
        - git clean -ffdx
    script:
        # files are in a subdirectory of the project
        - cd site
        - hugo --contentDir content/
          --config config/config.yaml
          --destination ../public/
    artifacts:
        paths:
            - public
        only:
            - tags
            - main

```

Now that you build your static site in GitLab, and deploy it to GitLab Pages, you can add your own domain to
GitLab pages by following a few steps.

Add your domain to GitLab Pages
--

Now we can add the domain to GitLab Pages. In your project, go to `Settings` > `Pages`. Here click the `New domain` button.

Fill in your domain, and set the `Automatic certificate management using Let's Encrypt` switch on.

{{< image "images/configure-gitlab-pages-domain" Fit "600x600" >}}
Configure your own domain in GitLab Pages settings.
{{< /image >}}

Verify your domain
---

To verify your domain, you will need to add two fields to your DNS. I am using [Google domains](https://domains.google), but it is all more or less the same.
All you need is privileges to alter the DNS settings of your domain.

Youl will have to add two records, so GitLab can verify you own the domain.

First you will have to add a `CNAME` record `<www.yourdomain.dev> CNAME <yourusername>.gitlab.io.` to forward the url to gitlab pages,
and a `TXT` record to verify the domain is yours `_gitlab-pages-verification-code.www.yourdomain.dev TXT gitlab-pages-verification-code=<somerandomcode>`.

{{< image "images/configure-google-dns" Fit "600x600" >}}
Configure dns records in google domains.
{{< /image >}}

Then hit the `verify` button. It might not work straight away because the records need to be synced. But in my case it was less than 5 minutes.

{{< image "images/gitlab-domain-not-verfied-failed.png" Fit "600x600" >}}
Before adding DNS records, domain fails to verify
{{< /image >}}

{{< image "images/gitlab-pages-domain-verify" Fit "600x600" >}}
Verify that the domain is yours after adding the verification code to your DNS
{{< /image >}}

If it worked, the status will change to verified

{{< image "images/gitlab-pages-domain-verified" Fit "600x600" >}}
Domain verified by GitLab.
{{< /image >}}

And in the overview, you will see that your domain is listed in the `Access pages section`

{{< image "images/gitlab-pages-domain-added" Fit "600x600" >}}
Domain added to GitLab Pages.
{{< /image >}}

Add a let's encrypt certificate to your page
--

Gitlab has this great help on how to use [let's encrypt](https://letsencrypt.org/) in combination with [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/).
Following the steps from [their manual](https://gitlab.com/help/user/project/pages/lets_encrypt_for_gitlab_pages.md#lets-encrypt-for-gitlab-pages) will get you all you need to register your https certificate to your domain.

**TL;DR;**

I had to register using [`certbot`](https://certbot.eff.org/). Just install the binary using the package manager of your OS.

```sh
certbot certonly -a manual -d www.forsure.dev --email hwdegroot@gmail.com
```

And it gave me the code in return of format `A.B`. Mine looked like

```sh
MXDCs3RTdKM5KNIJFbogSwTLoiduCbtyHKZ2k1zxvWQ.JEZ1UZmU4x3wCgSiV9gom4Irb8AgSkVFrsCju6sFLa8
```

then create a directory `public/.well-known/acme-challenge/A`, in my case `public/.well-known/acme-challenge/MXDCs3RTdKM5KNIJFbogSwTLoiduCbtyHKZ2k1zxvWQ/`.
Inside this directory, put a file `index.html` with the full `A.B` key in it, just as suggested by the certbot output

```sh
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
NOTE: The IP of this machine will be publicly logged as having requested this
certificate. If you're running certbot in manual mode on a machine that is not
your server, please ensure you're okay with that.

Are you OK with your IP being logged?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: y

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Create a file containing just this data:

MXDCs3RTdKM5KNIJFbogSwTLoiduCbtyHKZ2k1zxvWQ.JEZ1UZmU4x3wCgSiV9gom4Irb8AgSkVFrsCju6sFLa8

And make it available on your web server at this URL:

http://www.forsure.dev/.well-known/acme-challenge/TfBYIcpd4uO4y4kkH3GAYdsUXeCycAYLPcsF6JEiq1I

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

At this point, pause. **DO NOT** continue yet. If you did, no problem. Validation will fail, but the next time you run it, you will get the same code.

So the file `public/.well-known/acme-challenge/MXDCs3RTdKM5KNIJFbogSwTLoiduCbtyHKZ2k1zxvWQ/index.html` would look like

```html
<!-- index.html -->
MXDCs3RTdKM5KNIJFbogSwTLoiduCbtyHKZ2k1zxvWQ.JEZ1UZmU4x3wCgSiV9gom4Irb8AgSkVFrsCju6sFLa8
```

Basically that is it. You can continue the certificate registration, although it will probably fail. Make sure that GitLab deploys your
pages with the certificate directory `.well-known/acme-challenge/A` in it. You can check this by visiting `https://<your-domain>/.wel-known/acme-challenge/A/`. It should serve you this html page with the key in it. Then you can run the `certbot` command again, and it should present you the success message

```sh
IMPORTANT NOTES
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/blog.rikdegroot.dev/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/blog.rikdegroot.dev/privkey.pem
   Your cert will expire on 2019-10-17. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot
   again. To non-interactively renew *all* of your certificates, run
   "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
```

You're done!

Hope it helps

