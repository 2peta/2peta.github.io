---
layout: post
title: "Go練習: LookupHost"
description: ""
category:
tags: [golang]
---
{% include JB/setup %}

~~~ go
package main

import (
	"fmt"
	"net"
	"os"
)

func main() {
	name, err := os.Hostname()
	if err != nil {
		fmt.Printf("Oops: %v\n", err)
		return
	}
	fmt.Printf("hostname %s\n", name)

	addrs, err := net.LookupHost(name)

	if err != nil {
		fmt.Printf("Oops: %v\n", err)
		return
	}

	for _, a := range addrs {
		fmt.Println(a)
	}
}
~~~

* 自分のホスト名を得るには `os.Hostname()`を使う
* 得られたホスト名からIPアドレスを得るには`net.LookupHost(name)`を使う
  * `net.LookupHost`で得られるのはIPアドレスの配列。IPv4とv6が混在して文字列で返ってくる
  * どういう順序で返ってくるかはよくわからないが自分の環境ではv4が先だった
  
