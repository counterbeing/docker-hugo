# docker-hugo

Docker image for hugo static page generator (https://gohugo.io). This fork is based on [jojimi/docker-hugo](https://github.com/jojomi/docker-hugo). Except this is intended to be a sort of local wrapper for a system that might or might not already have `golang` installed.

This is just for executing hugo as you normally would if you had it installed. But instead it's wrapped in docker to keep it running consistently between development systems.

## Building The Image Yourself (optional)
Run `make build`.

## Creating a new tag
Checkout a branch, and run `make release`.

## docker-compose

Use this in your project to get hugo running.

`docker-compose.yml`

```yaml
hugo:
  image: counterbeing/hugo
  volumes:
    - .:/src
    - ./public/:/public
  ports:
    - "1313:1313"
  restart: always
```

I'd also recommend a `.env` file with [autoenv](https://github.com/kennethreitz/autoenv) to use hugo transparently in your project.

```bash
alias hugo='docker-compose run --service-ports hugo hugo'
```

Service ports are necessary here with the run command, or you won't be able to get to it with docker's run command.
