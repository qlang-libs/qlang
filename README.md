## qlang 

A dynamic programming language built for golang.

[qlang official repository(Chinese)](https://github.com/qiniu/qlang), English document is coming soon :-)


## qlang-libs

[qlang-libs](https://github.com/qlang-libs) contains a series of qlang packages to make our life easier.

### Install
1. qlang setup
	```shell
	cd $GOPATH/src
	mkdir qiniupkg.com
	git clone https://github.com/qiniu/qlang.git qlang.io
	git clone https://github.com/qiniu/text.git qiniupkg.com/text
	```

2. set qlang packages path env

	Add `export QLANG_PATH="$GOPATH/src/github.com/qlang-libs"` into `~/.bashrc` or `~/.zshrc`

	Although we recommend you to export `QLANG_PATH` to `$GOPATH/src/github.com/qlang-libs`, you can use any directory as your qlang packages directory, what the most important thing is that put all qlang packages into `$QLANG_PATH`.

### Quick start
1. qlang need a golang file to be executed

	```go
	package main

	import (
		"io/ioutil"
		"log"
		"os"

		"qlang.io/qlang.v2/qlang"
		qall "qlang.io/qlang/qlang.all"
	)

	func main() {
		qall.InitSafe(false)
		lang := qlang.New()
		lang.SetLibs(os.Getenv("QLANG_PATH"))

		// qlang source file path
		filePath := "play.ql"

		b, err := ioutil.ReadFile(*filePath)
		if err != nil {
			log.Panicln(err)
			return
		}

		err = lang.SafeExec(b, "")
		if err != nil {
			log.Panicln(err)
			return
		}
	}
	```

2. Write a qlang file importing [types](https://github.com/qlang-libs/types)

	1. Download the package

		```shell
		cd $QLANG_PATH
		git clone https://github.com/qlang-libs/types
		git clone https://github.com/qlang-libs/expectations
		```

	2. Create `play.ql` file

		```go
		import "types"
		slice = new types.Slice("int")	
		slice.push(1).push(2)
		println(slice.pop()) 
		// Outputs: 2
		```



