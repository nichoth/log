## keys and identity in ssb

[Each ssb feed is signed with a public key](https://ssbc.github.io/secure-scuttlebutt/). What does that mean?

[link](https://stackoverflow.com/questions/18257185/how-does-a-public-key-verify-a-signature)

A digital signature is a hash of the content that is encrypted with the signer's private key. The hash is then decrypted with the public key (which the recipient has).

The example ssb message has a signature, and I'm guessing the `author` field is the public key.

```
{
  "previous": "%26AC+gU0t74jRGVeDY013cVghlZRc0nfUAnMnutGGHM=.sha256",
  "author": "@hxGxqPrplLjRG2vtjQL87abX4QKqeLgCwQpS730nNwE=.ed25519",
  "sequence": 216,
  "timestamp": 1442590513298,
  "hash": "sha256",
  "content": {
    "type": "vote",
    "vote": {
      "link": "%WbQ4dq0m/zu5jxll9zUbe0iGmDOajCx1ZkLKjZ80JvI=.sha256",
      "value": 1
    }
  },
  "signature": "Sjq1C3yiKdmi1TWvNqxIk1ZQBf4pPJYl0HHRDVf/xjm5tWJHBaW4kXo6mHPcUMbJYUtc03IvPwVqB+BMnBgmAQ==.sig.ed25519"
}
```

-----------------------------------------

[ssb concepts](https://github.com/ssbc/ssb-handbook/blob/master/concepts/index.md)

>  the connections between humans maps approximately to the the connections between computers

[guide to sbot](https://github.com/ssbc/ssb-handbook/blob/master/guides/cli-first-steps.md) an ssb cli

> The first time you run Scuttlebot (or an application using it), an identity is created (in the form of a public and private key pair)

Scuttlebot is an ssb peer that runs on a server. You can use it to maintain a connection to the greater ssb network. It comes with a command line tool `sbot` that does some useful things like printing feeds of messages.

This example shows a message of type `about`, used to associate the name "arithmetric" with a public key (the value of `value.content.about`).

```js
$ sbot createUserStream --id "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519" --limit 1
{
  "key": "%S/nfXzDK3waYEaEDwwGA7FsIqFzpIiU3200Lf0aG/Ps=.sha256",
  "value": {
    "previous": null,
    "author": "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519",
    "sequence": 1,
    "timestamp": 1491533348827,
    "hash": "sha256",
    "content": {
      "type": "about",
      "about": "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519",
      "name": "arithmetric"
    },
    "signature": "B/I1k24ihHsivqzo+G01M/rqQWCIC8YYlt7+EiKoovdd1C36b8/RU+DgFO80lzNNPWWakgh9K+vY2hdslelMAQ==.sig.ed25519"
  }
}
```


This is an example of an encrypted private message. The `content` field has been encrypted with the public key of another user.

```js
{
  "previous": "%jhaGHJiDINuSp1gr6nHbxhB9BCW9HIPtGR3ntdN3EWM=.sha256",
  "author": "@btxEYD1gibOZZKbtxJFTQ2m560U3zIgbZ2vII93WCIk=.ed25519",
  "sequence": 23,
  "timestamp": 1491611316858,
  "hash": "sha256",
  "content": "cZOlfY2YQBMqIKkX7zKwnlZ8eC2gElbmk2HOoXGW/tkYberzSW3k3rw1XJxuJKavmSHNCF9e4hWVCueIFa2ibFOxxkuEy13rYk1YGmWj4xgxx1Vv4hUuLIsdeRM50XH+7OTkAejkc2pu+4NYXZDbmuINX8djUrddjwq3VDUbk...",
  "signature": "gYceZ6gv7Kd2L78uCYsEwro/q8Y+BNSyeNoSshtIbfN4T6ZZ3bz5JyU8qt/q4ecNSaSjj1pxaGM+UQ9NOsdQDQ==.sig.ed25519"
}
```



