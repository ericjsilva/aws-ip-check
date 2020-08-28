# AWS IP Checker [![Build Status](https://travis-ci.org/ericjsilva/aws-ip-check.svg?branch=master)](https://travis-ci.org/ericjsilva/aws-ip-check)

`aws-ip-check` is a command line tool to check if an IP address belongs to Amazon Web Service (AWS) infrastructure or not.

This tool relies on public [AWS IP range file](https://ip-ranges.amazonaws.com/ip-ranges.json).

## Installation

Make sure you have a working Go environment.

To install `aws-ip-check` cli, simply run:

```shell
$ go get github.com/ericjsilva/aws-ip-check/cmd/aws-ip-check
```

## Usage

```shell
$ aws-ip-check help
usage: aws-ip-check [flags]
  -ip string
      IP address to check if belongs to AWS
  -path string
      File path to store AWS ip-ranges.json (default "/tmp/aws-ip-ranges.json")
```

`aws-ip-check` will return the following exit statuses:

| status | description |
| ---: | --- |
| 0 | IP belongs to AWS IP range |
| 1 | IP does NOT belong to AWS IP range |
| 2 | aws-ip-check execution error |

## Example

```shell
$ aws-ip-check -ip 192.168.1.1
IP 192.168.1.1 not found in AWS IP range


$ aws-ip-check -ip $(nslookup www.amazon.com  | grep "Address" | tail -1 | awk '{print $NF}')
IP X.X.X.X found in AWS IP range for region {region}.
```
