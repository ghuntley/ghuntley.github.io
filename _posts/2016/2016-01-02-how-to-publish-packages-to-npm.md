---
layout:     post
title:      How to publish packages to NPM
date:       2016-01-02
summary:    A quick overview/rundown on how to setup NPM, create and publish a package.
categories: npm javascript package-management
---

If you haven't already set your NPM author info, here's how you do it:

```shell
# npm set init.author.name "Your Name"
# npm set init.author.email "you@example.com"
# npm set init.author.url "http://yourblog.com"
```

If you don't have an NPM account, one can be created by running

```shell
# npm adduser
```

Next steps are to create your `package.json`:

```shell
# cd /path/to/your-project
# npm init
```

If you took on dependencies, then you should install and run pakmager.
```shell
# npm install -g pakmanager
# pakmanager deps
```

Edit your package.json and add any deps you forgot about.
```shell
# vim package.json
```

Publish your libary.

```shell
# npm publish ./ --tag beta
# npm publish ./
```

Additional reading:

  * http://npmjs.org/doc/json.html
  * http://npmjs.org/doc/developers.html
  * http://blog.izs.me/post/1675072029/10-cool-things-you-probably-didnt-realize-npm-could-do
