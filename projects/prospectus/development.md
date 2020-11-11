---
layout: default
title: Implementation
parent: Supplier Prospectus
nav_order: 2
last_modified_date:  2020-11-08 15:26:12 UTC
share: Prototyping a Supplier Prospectus
---

# Implementation
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Overview

The application is primarily written in Golang, with some use of CGo (see
below).  Java is used for processing XSL Formatting Objects documents. The
application runs on an Arm-based AWS Graviton2 EC-2 instance, pretty
comfortably (at the moment) using a t4g.micro instance.

We've made a few of the components available through public respositories on
GitHub, under the MIT license (a permissive open source license). These
components are described below.

## GO-XSLT: XSL Transformations in Golang 

<a href="https://github.com/wamuir/go-xslt"><i class='fa
fa-github'></i>&nbsp;GitHub repo</a>

Golang has an XML package (`encoding/xml`) that can parse XML 1.0, marshal and
unmarshal to structs.  There is, however, no built-in support for XSLT. We
needed to perform XSL transformations for our [prospector
prototype](/projects/prospectus/), and decided against `os/exec` calls, for
instance, to `xsltproc`.

Enter [Cgo](https://golang.org/cmd/cgo/) and the venerable
[Libxslt](http://xmlsoft.org/libxslt/) for XSLT 1.0 transformations.  This Go
library parses and stores stylesheets in memory, which can be reused for
subsequent transformations.


### Usage
{: .no_toc }


```go
  // style is an XSLT 1.0 stylesheet, as []byte.
  xs, err := xslt.NewStylesheet(style)
  if err != nil {
      panic(err)
  }
  defer xs.Close()

  // doc is an XML document to be transformed and res is the result of
  // the XSL transformation, both as []byte. 
  res, err := xs.Transform(doc)
  if err != nil {
      panic(err)
  }
```


## SVG-QR-CODE: Scalable Vector Graphics encoding of Quick Response Codes

<a href="https://github.com/wamuir/svg-qr-code"><i class='fa
fa-github'></i>&nbsp;GitHub repo</a>

Quick Response (QR) codes are commonly used to provide easy access to websites
(among their other uses), given mobile phone support for scanning these
barcodes.  We wanted to provide mechanisms for a supplier prospectus to be
easily refreshed (i.e., to generate a new prospectus), that could be used when
the document is in electronic and print forms.  Hyperlinks easily solve the
electronic case.  An idea, currently implemented, for allowing easy refreshes
of the printed document is to include a QR code.  This project relies on
[go-qrcode](https://github.com/skip2/go-qrcode) to build the code as
`image.Image`, and then iterates over the pixel matrix to create Go structs
which can later be marshaled to SVG (XML).


### Usage
{: .no_toc }


```go
  qr, err := qrsvg.New("https://github.com/wamuir/svg-qr-code")
  if err != nil {
     panic(err)
  }

  // qr satisfies fmt.Stringer interface (or call qr.String() for a string)
  fmt.Println(qr)
```

## SIMPLE-FOP-SERVER: Simply an Apache FOP server for simple cases

<a href="https://github.com/wamuir/simple-fop-server"><i class='fa
fa-github'></i>&nbsp;GitHub repo</a>

There isn't much to say here, it's a HTTP server that processes XSL-FO using
[Apache FOP](https://xmlgraphics.apache.org/fop/).

### Usage
{: .no_toc }
```console
toor@box~$ docker build -t fop . && docker run -it fop
```
