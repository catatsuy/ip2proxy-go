[![Go Report Card](https://goreportcard.com/badge/github.com/ip2location/ip2proxy-go)](https://goreportcard.com/report/github.com/ip2location/ip2proxy-go)

# IP2Proxy Go Package

This package allows user to query an IP address if it was being used as VPN anonymizer, open proxies, web proxies, Tor exits, data center, web hosting (DCH) range and search engine robots (SES). It lookup the proxy IP address from **IP2Proxy BIN Data** file. This data file can be downloaded at

* Free IP2Proxy BIN Data: https://lite.ip2location.com
* Commercial IP2Proxy BIN Data: https://www.ip2location.com/database/ip2proxy


## Installation

To install this module type the following:

```bash

go get github.com/ip2location/ip2proxy-go

```

## Methods
Below are the methods supported in this package.

|Method Name|Description|
|---|---|
|Open|Open the IP2Proxy BIN data for lookup.|
|Close|Close and clean up the file pointer.|
|PackageVersion|Get the package version (1 to 8 for PX1 to PX8 respectively).|
|ModuleVersion|Get the module version.|
|DatabaseVersion|Get the database version.|
|IsProxy|Check whether if an IP address was a proxy. Returned value:<ul><li>-1 : errors</li><li>0 : not a proxy</li><li>1 : a proxy</li><li>2 : a data center IP address or search engine robot</li></ul>|
|GetAll|Return the proxy information in an array.|
|GetProxyType|Return the proxy type. Please visit <a href="https://www.ip2location.com/database/px8-ip-proxytype-country-region-city-isp-domain-usagetype-asn-lastseen" target="_blank">IP2Location</a> for the list of proxy types supported.|
|GetCountryShort|Return the ISO3166-1 country code (2-digits) of the proxy.|
|GetCountryLong|Return the ISO3166-1 country name of the proxy.|
|GetRegion|Return the ISO3166-2 region name of the proxy. Please visit <a href="https://www.ip2location.com/free/iso3166-2" target="_blank">ISO3166-2 Subdivision Code</a> for the information of ISO3166-2 supported.|
|GetCity|Return the city name of the proxy.|
|GetIsp|Return the ISP name of the proxy.|
|GetDomain|Return the domain name of the proxy.|
|GetUsageType|Return the usage type classification of the proxy. Please visit <a href="https://www.ip2location.com/database/px8-ip-proxytype-country-region-city-isp-domain-usagetype-asn-lastseen" target="_blank">IP2Location</a> for the list of usage types supported.|
|GetAsn|Return the autonomous system number of the proxy.|
|GetAs|Return the autonomous system name of the proxy.|
|GetLastSeen|Return the number of days that the proxy was last seen.|

## Usage

```go
package main

import (
	"fmt"
	"github.com/ip2location/ip2proxy-go"
)

func main() {
	if ip2proxy.Open("./IP2PROXY-IP-PROXYTYPE-COUNTRY-REGION-CITY-ISP-DOMAIN-USAGETYPE-ASN-LASTSEEN.BIN") == 0 {
		ip := "199.83.103.79"
		
		fmt.Printf("ModuleVersion: %s\n", ip2proxy.ModuleVersion())
		fmt.Printf("PackageVersion: %s\n", ip2proxy.PackageVersion())
		fmt.Printf("DatabaseVersion: %s\n", ip2proxy.DatabaseVersion())
		
		// functions for individual fields
		fmt.Printf("IsProxy: %d\n", ip2proxy.IsProxy(ip))
		fmt.Printf("ProxyType: %s\n", ip2proxy.GetProxyType(ip))
		fmt.Printf("CountryShort: %s\n", ip2proxy.GetCountryShort(ip))
		fmt.Printf("CountryLong: %s\n", ip2proxy.GetCountryLong(ip))
		fmt.Printf("Region: %s\n", ip2proxy.GetRegion(ip))
		fmt.Printf("City: %s\n", ip2proxy.GetCity(ip))
		fmt.Printf("ISP: %s\n", ip2proxy.GetIsp(ip))
		fmt.Printf("Domain: %s\n", ip2proxy.GetDomain(ip))
		fmt.Printf("UsageType: %s\n", ip2proxy.GetUsageType(ip))
		fmt.Printf("ASN: %s\n", ip2proxy.GetAsn(ip))
		fmt.Printf("AS: %s\n", ip2proxy.GetAs(ip))
		fmt.Printf("LastSeen: %s\n", ip2proxy.GetLastSeen(ip))
		
		// function for all fields
		all := ip2proxy.GetAll(ip)
		fmt.Printf("isProxy: %s\n", all["isProxy"])
		fmt.Printf("ProxyType: %s\n", all["ProxyType"])
		fmt.Printf("CountryShort: %s\n", all["CountryShort"])
		fmt.Printf("CountryLong: %s\n", all["CountryLong"])
		fmt.Printf("Region: %s\n", all["Region"])
		fmt.Printf("City: %s\n", all["City"])
		fmt.Printf("ISP: %s\n", all["ISP"])
		fmt.Printf("Domain: %s\n", all["Domain"])
		fmt.Printf("UsageType: %s\n", all["UsageType"])
		fmt.Printf("ASN: %s\n", all["ASN"])
		fmt.Printf("AS: %s\n", all["AS"])
		fmt.Printf("LastSeen: %s\n", all["LastSeen"])
	} else {
		fmt.Printf("Error reading BIN file.\n")
	}
	ip2proxy.Close()
}
```
