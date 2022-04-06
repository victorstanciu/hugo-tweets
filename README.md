# Static user timeline for Hugo

I made this plugin for Hugo because I wanted a way to embed my own Twitter timeline on [my blog](https://tegowerk.eu) without having to load any external scripts or images. All it does is fetch the tweets via Twitter's own API and render them on each `hugo build`.

**Note:** It's important to run `hugo build` with the `--ignoreCache` parameter, otherwise fresh tweets won't show up, as the API responses get cached.

## Prerequisites

You will first need to obtain an [OAauth Bearer (app-only) token](https://developer.twitter.com/en/docs/authentication/oauth-2-0) from Twitter. For this you will need a developer account and an application.

Once you have this token, you will need to make it accessible as an environment variable called `HUGO_TWITTER_API_TOKEN` for the `hugo` executable. There are plenty of guides online on how to do that for your operating system of choice, so I won't repeat that information here.

## How to install

Download or clone this repository into your `/themes` directory:

```
git clone git@github.com:victorstanciu/hugo-tweets.git
```

Edit your `config.toml`, `config.yaml`, or `config.json` file to load the theme **before** your other theme(s):

```
theme = ["hugo-tweets", "minima"]
```

## How to embed

There are two ways to embed the timeline:

- As a shortcode (in `/content/*.md` files):

    ```
    {{< stimeline username="[USERNAME]" results=10 >}}
    ```

- As a partial (in `/layout/*.html` files):

    ```
    {{ .Scratch.Set "twitter_username" "[USERNAME]" }}
    {{ .Scratch.Set "twitter_results" 10 }}
    {{ partial "stimeline.html" . }}
    ```