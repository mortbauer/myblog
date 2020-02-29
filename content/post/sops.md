---
title: "Sops"
date: 2019-05-29T21:09:00+02:00
draft: false
tags: [security, encryption]
---

# Intro to [sops](https://github.com/mozilla/sops)

This is just a very quick intro to sops an open sourced secrets management tool
from mozilla.

Sops can be used to transparently encrypt full, or partially config files,
transparently in the sense that the keys in a yaml, json won't be
encrypted only the values, which allows to version control the file with
git and more.

To create an with your gpg key 'encrypted' file run:

```
sops -p $(gpg --fingerprint mymail@whatever.com | sed -n '2p' | tr -d ' ') test.dev.yaml
```

Which basically gets your fingerprint without spaces, you will have to modify
your email address, and uses it to create a datakey which in turn then is used
to encrypt the values of that yaml file. 

To decrypt the file use: `sops -d test.dev.yaml`

The beauty is that one can use several different keys which can then all, or
all together depending on the configuration, used to decrypt the values.

One can also selectively only encrypt the values of some keys or not.

This can be easily managed with a .sops.yaml, the .sops.yaml for our example
would look the following:


```
creation_rules:
    - path_regex: .*\.dev\.yaml
      pgp: 'EA68F1F245C64189B0BDA3EA0E67E12E45D98394'
      encrypted_suffix: secret
```


For more info checkout [sops](https://github.com/mozilla/sops) which also has a
nice introduction video.
