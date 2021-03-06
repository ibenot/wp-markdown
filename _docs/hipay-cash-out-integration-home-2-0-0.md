---
ID: 542
post_title: 1. Home
author: ibenot
post_date: 2016-04-05 10:32:15
post_excerpt: ""
layout: documentation
permalink: >
  http://bnotteghem.com/dev/doc/hipay-cash-out-integration-home-2-0-0/
published: true
language:
  - PHP
tag:
  - 2.0.0
chapter:
  - 1. Home
product:
  - HiPay Wallet
techno:
  - Mirakl
---
![HiPay cash-out integration for Mirakl](https://github.com/hipay/hipay-wallet-cashout-mirakl-integration/wiki/images/header.jpg)

# HiPay cash-out integration for Mirakl 2.0.0

## Preamble
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