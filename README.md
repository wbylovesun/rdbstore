# rdbstore

[//]: # ()
[//]: # ([![GoDoc]&#40;https://godoc.org/github.com/boj/redistore?status.svg&#41;]&#40;https://godoc.org/github.com/boj/redistore&#41;)

[//]: # ([![Build Status]&#40;https://travis-ci.org/boj/redistore.svg?branch=master&#41;]&#40;https://travis-ci.org/boj/redistore&#41;)

A session store backend for [gorilla/sessions](http://www.gorillatoolkit.org/pkg/sessions) - [src](https://github.com/gorilla/sessions).

This project comes from boj/redistore. For some reason, that project has no reviewer to keep it fresh, so decided to fork a new one to rebuild it.

All rights belongs to boj/redistore, and license never changed, but new mod name is github.com/wbylovesun/rdbstore.

## Requirements

Depends on the [Redigo](https://github.com/gomodule/redigo) Redis library.

## Installation

    go get gopkg.in/boj/redistore.v1

## Documentation

Available on [godoc.org](http://www.godoc.org/gopkg.in/boj/redistore.v1).

See http://www.gorillatoolkit.org/pkg/sessions for full documentation on underlying interface.

### Example
``` go
// Fetch new store.
store, err := NewRediStore(10, "tcp", ":6379", "", []byte("secret-key"))
if err != nil {
	panic(err)
}
defer store.Close()

// Get a session.
session, err = store.Get(req, "session-key")
if err != nil {
	log.Error(err.Error())
}

// Add a value.
session.Values["foo"] = "bar"

// Save.
if err = sessions.Save(req, rsp); err != nil {
	t.Fatalf("Error saving session: %v", err)
}

// Delete session.
session.Options.MaxAge = -1
if err = sessions.Save(req, rsp); err != nil {
	t.Fatalf("Error saving session: %v", err)
}

// Change session storage configuration for MaxAge = 10 days.
store.SetMaxAge(10 * 24 * 3600)
```
