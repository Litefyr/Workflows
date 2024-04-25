# Workflows for [Litespeed] and [Neos]

## How to use it

You can either directly reference to this workflows, copy this repository, and change it to your needs, or copy the
steps into your own workflow file. Just as you want. Take a look at the [Distribution] on an example workflow

## Workflows

### Build workflow

As you shouldn't store any imported or builded files, this workflows download and install your [composer] and
[node dependencies], build the needed JavaScript and CSS Files with the script `pipeline` defined in your `package.json`,
and uploads them to an artifact named `build`.

#### Authentication for composer

The `COMPOSER_AUTH` secret allows you to set up authentication as an environment variable. The contents of the variable
should be a `JSON` formatted object containing [http-basic, github-oauth, bitbucket-oauth, … objects][authentication]
as needed, and following the [spec from the config][composer config].

#### Define which files should be uploaded

With the variable `upload`, you can define which files and folders should be uploaded to the artifact. No worry, if you
have one file missing, the action doesn't fail because of that. All you get is a warning in the console. As [Litespeed]
is capable of updating your `CSS` as some markup changes, it uploads per default also the build stack from [Carbon.Pipeline]

### Docker workflow

We use docker on our hosting, we give you also this workflow. To be able to upload the image to the GitHub Docker Hub,
you'll need to set the secrets `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN`.

There are several variables:

| Name         | Description                              | Default                     |
| ------------ | ---------------------------------------- | --------------------------- |
| `tags`       | Tags for docker image (required)         |                             |
| `artifact`   | Name of the artifact to download & build | `build`                     |
| `platforms`  | Platforms for docker image               | `linux/amd64`               |
| `dockerfile` | Dockerfile to use                        | `./.docker/neos/Dockerfile` |

[litespeed]: https://litespeed.io
[neos]: https://neos.io
[distribution]: https://github.com/LitespeedProject/Distribution
[composer]: https://getcomposer.org
[node dependencies]: https://www.npmjs.com
[authentication]: https://getcomposer.org/doc/articles/authentication-for-private-packages.md
[composer config]: https://getcomposer.org/doc/06-config.md
[Carbon.Pipeline]: https://github.com/CarbonPackages/Carbon.Pipeline
