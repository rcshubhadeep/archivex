archivex
========

archivex is a golang package that archives folders (recursively) and files to zip and tar formats.

With a capability to selectively archieve files if given the names of the files to ignore at the time of archieving. 

[![Build Status](https://travis-ci.org/jhoonb/archivex.svg)](https://travis-ci.org/jhoonb/archivex) 
[![](http://gocover.io/_badge/github.com/jhoonb/archivex)](http://gocover.io/github.com/jhoonb/archivex)

Installation
-------------

``` bash
$ go get github.com/jhoonb/archivex
``` 


Example 
-------------

```go 

package main

import (
	"github.com/jhoonb/archivex"
)

// Example using only func zip
func zip() {
	zip := new(archivex.ZipFile)
	zip.AddIgnores([]string{"blabla.txt", "blabla2.txt"}) //If you want to add some files in the ignore list
	zip.Create("filezip")
	zip.Add("testadd.txt", []byte("test 1"))
	zip.AddFile("<input_path_file_here>")
	zip.AddAll("<input_dir_here>", true)
	zip.Close()
}

// Example using only func tar
func tar() {
	tar := new(archivex.TarFile)
	tar.AddIgnores([]string{"blabla.txt", "blabla2.txt"}) //If you want to add some files in the ignore list
	tar.Create("filetar")
	tar.Add("testadd.txt", []byte("test 1"))
	tar.AddFile("<input_path_file_here>")
	tar.AddAll("<input_dir_here>", true)
	tar.Close()
}

// Example using interface
func usingInterface() {

	archx := []archivex.Archivex{&archivex.TarFile{}, &archivex.ZipFile{}}

	for _, arch := range archx {
		arch.Create("fileinterface")
		arch.AddIgnores([]string{"blabla.txt", "blabla2.txt"}) //If you want to add some files in the ignore list
		arch.Add("testadd.txt", []byte("file 1 :) "))
		arch.AddFile("<input_path_file_here>")
		arch.AddAll("<input_dir_here>", true)
		arch.Close()
	}
}

func main() {

	zip()
	tar()
	usingInterface()
}

```

:)
