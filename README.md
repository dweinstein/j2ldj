# SYNOPSIS

A very handy and narrowly scoped utility to take the output from [JSONStream](https://github.com/dominictarr/JSONStream) for piping into tools like [jq](https://github.com/stedolan/jq).

Tools like `jq` will otherwise hang waiting.

Basically it takes

```javascript
[\n
{"field": "value"}\n
,\n
{"field": "value"}\n
... lots and lots of objects ...
,\n
]\n
```

and makes it into:

```javascript
{"field": "value"}\n
{"field": "value"}\n
... lots and lots of objects ...
```


## motivation
Let's say you have a very large source of JSON, maybe it's in a file; maybe it's something sending data over an http connection and that data has been piped through `JSONStream`.

On the receiving end it looks like this:

```javascript
[
{"field": "value"}
,
... lots and lots of objects ...
,
]
```

Now if you pipe this directly to `jq` it waits for the closing `]` before it'll start outputting the stream.

This made me sad.

# USAGE

```sh
npm install -g j2ldj
```

```sh
curl localhost/big_json_response | j2ldj | jq '.'
```
