This is a Go implementation of the Google Authenticator library.

[![GoDoc](https://godoc.org/github.com/dgryski/dgoogauth?status.svg)](https://godoc.org/github.com/dgryski/dgoogauth) [![Build Status](https://travis-ci.org/dgryski/dgoogauth.png)](https://travis-ci.org/dgryski/dgoogauth)

Copyright (c) 2012 Damian Gryski <damian@gryski.com>
This code is licensed under the Apache License, version 2.0

It implements the one-time-password algorithms specified in:

* RFC 4226 (HOTP: An HMAC-Based One-Time Password Algorithm)
* RFC 6238 (TOTP: Time-Based One-Time Password Algorithm)

You can learn more about the Google Authenticator library at its project page:

* https://github.com/google/google-authenticator

示例：

	username := "a@a.com"
	password := "aaaa"
	token := md5V(username + "#" + password)
	otp := new(OTPConfig)
	//添加WithPadding(base32.NoPadding) 否则生成的二维码 app认为无效，对应的检验方法里也要加上这个	  	
    otp.Secret = base32.StdEncoding.WithPadding(base32.NoPadding).EncodeToString([]byte(token))
	//把这个url生成二维码就可以了	
    fmt.Println(otp.ProvisionURIWithIssuer(username, "360stack"))

	p := os.Args[1]
    //校验通过
	res, _ := otp.Authenticate(p)
	fmt.Println(res)
