cursedjson
==========

[![GoDoc](https://godoc.org/github.com/q3k/cursedjson?status.svg)](https://godoc.org/github.com/q3k/cursedjson)

A drop-in replacement for `encoding/json` when you absolutely, positively need to decode JSON files that contain Infinity, -Infinity and NaN.

This is useful for when you're interfacing with a brain dead system that uses `json.dump()` in Python without setting `allow_nan=False`. Because by default, it will be non-compliant with the JSON RFC that Go follows.

Fuck JSON, by the way.

Usage
-----

    import "github.com/q3k/cursedjson"

    t := struct {
        ExampleInfinity  float64 `json:"infinity"`
        ExampleNInfinity float64 `json:"ninfinity"`
        ExampleNaN       float64 `json:"nan"`
    }{}
    
    err := Unmarshal([]byte{`{"infinity": Infinity, "ninfinity": -Infinity, "nan": NaN}`}, &t)
    if err != nil {
        panic(err)
    }
    
    fmt.Printf("%+v\n", t)

License
-------

    // Copyright 2010 The Go Authors. All rights reserved.                                                                      
    // Copytight 2019 Serge Bazanski. All rights reserved.
    // Use of this source code is governed by a BSD-style
    // license that can be found in the LICENSE file.

