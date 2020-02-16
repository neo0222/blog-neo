# Blog - Nuxt.js + Contentful

- Blog: https://blog-neo.com/
- Qiita: https://qiita.com/neo0222
- blog-neo.com(Terraform): https://github.com/neo0222/blog-neo-terraform

## Build Setup

``` bash
# install dependencies
$ docker-compose run --rm node yarn install

# serve with hot reload at localhost:3000 after a few seconds later
$ docker-compose up

# generate static project
$ docker-compose run --rm node yarn run generate

# develop without docker
$ cross-env NODE_ENV=development CTF_SPACE_ID=vrsagmse1qfb CTF_CDA_ACCESS_TOKEN=5d3d838e7be39328a3f20175aafa937201e308d0bb10498d3283361db3aa1654 yarn run dev
```
