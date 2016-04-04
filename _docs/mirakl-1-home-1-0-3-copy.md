---
ID: 495
post_title: 1. Home Copy
author: ibenot
post_date: 2016-04-04 15:09:40
post_excerpt: ""
layout: documentation
permalink: >
  http://bnotteghem.com/dev/doc/mirakl-1-home-1-0-3-copy/
published: true
language: [ ]
tag: [ ]
chapter: [ ]
product: [ ]
techno: [ ]
---
![Mirakl](https://github.com/hipay/hipay-wallet-cashout-mirakl-integration/wiki/images/header.jpg)

## Preamble Mirakl 1.0.3
The **HiPay Wallet cash-out integration for Mirakl** intends to facilitate cash-out operations between HiPay and the Mirakl marketplace solution. Please note that this software is a turnkey integration of the [HiPay Wallet cash-out library for Mirakl][repo-lib], which is useless alone and needs to be integrated. In most cases, you won't need to integrate the library yourself. So unless you have specific needs, you're in the right place.

## Objective
This integration is a standalone application software that will, once set up, handle cash-out operations. This is done by automatically retrieving the payment orders from Mirakl and sending them to HiPay for withdrawal both to the merchants' and the marketplace operator's bank accounts. 

## Table of contents
1. [[Disclaimer]]
2. [[Prerequisites and recommendations]]
3. [[Mirakl account configuration]]
4. [[Installation]]
5. [[Usage]]
6. [[Parameters]]

[repo-lib]: https://github.com/hipay/hipay-wallet-cashout-mirakl-library