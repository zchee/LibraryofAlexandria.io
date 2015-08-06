+++
date = "2015-07-22T07:03:16+09:00"
title = "gem install eventmachineがopenssl.hがなくて失敗するとき"

+++

## gem install eventmachineがopenssl.hがなくて失敗するとき
http://stackoverflow.com/questions/30818391/gem-eventmachine-fatal-error-openssl-ssl-h-file-not-found

```
gem install eventmachine -v '1.0.7' -- --with-cppflags=-I/usr/local/opt/openssl/include
```
