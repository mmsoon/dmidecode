# dmidecode
![Build and Test](https://github.com/mmsoon/dmidecode/workflows/Build%20and%20Test/badge.svg)
[![codecov](https://codecov.io/gh/mmsoon/dmidecode/branch/master/graph/badge.svg)](https://codecov.io/gh/mmsoon/dmidecode)
[![Go Report Card](https://goreportcard.com/badge/github.com/mmsoon/dmidecode)](https://goreportcard.com/report/github.com/mmsoon/dmidecode)
[![Release](https://img.shields.io/github/release/mmsoon/dmidecode.svg?style=flat-square)](https://github.com/mmsoon/dmidecode/releases)
[![MIT License](https://img.shields.io/github/license/mmsoon/dmidecode.svg)](https://github.com/mmsoon/dmidecode/blob/master/LICENSE)

纯Golang实现的dmidecode, 零依赖, 支持Linux, Unix, Windows

功能和命令行的dmidecode工具一样, 使用方式参考: [example](./example/main.go)

开发过程相关小博客: [使用Golang重新实现dmidecode](https://www.jianshu.com/p/2e7ce2946b6b)

## 安装方式

```
$ go get "github.com/mmsoon/dmidecode"
```

## 使用样例

``` go
package main

import (
	"fmt"
	"os"

	"github.com/mmsoon/dmidecode"
)

func checkError(err error) {
	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}
}

func main() {
	dmi, err := dmidecode.New()
	checkError(err)

	infos, err := dmi.BIOS()
	// 支持以下类型的解析
	// dmi.BaseBoard()
	// dmi.Chassis()
	// dmi.MemoryArray()
	// dmi.MemoryDevice()
	// dmi.Onboard()
	// dmi.PortConnector()
	// dmi.Processor()
	// dmi.ProcessorCache()
	// dmi.Slot()
	// dmi.System()
	checkError(err)

	for i := range infos {
		fmt.Println(infos[i])
	}
}
```

## CLI 使用
``` sh
$ go run cmd/main.go -d -t [bios, system, baseboard, chassis, onboard, port, processor, memory, slot]
```