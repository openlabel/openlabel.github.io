---
layout: post
title: Heartbleed
cover: cover.png
date:   2013-04-10 12:00:00
categories: posts
tags: engineering
---

## Heartbleed

By now you may have caught wind of the Heartbleed OpenSSL vulnerability (<a href="https://www.openssl.org/news/secadv_20140407.txt">CVE-2014-0160</a>).

## Mitigating Heartbleed at OpenLabel

Our servers have been upgraded with the patched libraries as of 8th April, 2014.

In addition, our servers have <a href="https://www.eff.org/deeplinks/2014/04/why-web-needs-perfect-forward-secrecy">Forward Secrecy</a> (or Perfect Forward Secrecy) enabled since the beginning of 2014, which greatly mitigates user data being decrypted in the case of the private key being exposed.

As a precaution, we will re-key and re-issue our sercurity certificates.

We urge all OpenLabel users to update their passwords a precaution.

Note: we are not aware of any compromised data due to the Heartbleed vulnerability.

To check the security of our service, you can use Qualy's SSL Labs excellent <a href="https://www.ssllabs.com/ssltest/analyze.html?d=theopenlabel.com">SSL Server Test</a> tool.