[ssb tutorial](https://ssbc.github.io/docs/scuttlebot/tutorial.html)

Make a ssb app.

* Use scuttlebot as a server. If two apps embed scuttlebot on the same machine, it will cause conflicts

* scuttlebot's cli, `sbot` maps shell commands directly to RPC calls

* the client code can use `ssb-client` to load the device's ssb keypair

* publish a message
```js
sbot.publish({ type: 'post', text: 'hello, world' }, cb)
```

* messages:
  * must include `type` field
  * output message, including headers, cannot exceed 8kb

* take a look at [existing messages schemas](https://github.com/ssbc/ssb-msg-schemas)

* sbot has a separate blob store. The messages link to the blobs by the hash of the file content
```js
sbot.blobs.add(function (err, fileId) {})
```

* the order of messages is not preserved between different feeds

* scuttlebot's internal APIs will validate everything in `msg.value.*` except for `msg.value.content.*`. That's up to the application.

* When you expect an attribute to be a link, you can handle it with ssb-msgs link functions



