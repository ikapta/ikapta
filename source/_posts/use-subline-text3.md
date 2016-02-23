title: use subline text3
date: 2015-08-9 01:36:34
tags: [subline,licence]
---

 - 初始化下载 [官网地址][1]
 
 - licence
 <!-- more -->
 ``` javascript
     ----- BEGIN LICENSE -----
    Fred Zirdung
    Single User License
    EA7E-844672
    6089C0EC 22936E1A 1EADEBE2 B8654BBA
    5C98FFA6 C0FD1599 0364779B 071C74FB
    EEFE9EAB 92B3D867 CD1B32FE D190269F
    6FC08F8F 8D24191D 32828465 942CE58E
    AECE5307 08B62229 D788560A 6E0AAC4B
    48A2D9EE 24FD8CAA 07BEBDF2 28EA86D4
    CCB96084 6C34CAD2 E8A04F39 3B5A3CBC
    3B668BB7 C94D0B4B 847D6D7F 4BC07375
    ------ END LICENSE ------
     
    ----- BEGIN LICENSE -----
    Wixel
    Single User License
    EA7E-848235
    103D2969 8700C7ED 8173CF61 537000C0
    EB3C7ECB 5E750F17 6B42B67C A190090B
    7669164F C6F371A8 5A1D88D5 BDD0DA70
    C065892B 7CC1BB2B 1C8B8C7C F08E7789
    7C2A5241 35F86328 4C8F70D9 C023D7C2
    11245C36 59A730DB 72BDB9A7 D5B20304
    90E90E72 9F08CA25 73F49C20 179D938E
    5BC8BEDA 13457A69 39E6265F 233767F9
    ------ END LICENSE ------
     
    ----- BEGIN LICENSE -----
    Daniel Russel
    Single User License
    EA7E-917420
    9327EC62 44020C2A 45172A68 12FE13F1
    1D22245B 680892EE F551F8EB C183D032
    8B4EDB4B 479CB7E4 07E42EDD A780021D
    56BADF42 AC05238B 023B47B1 EBA1B7DE
    6DF9A383 159F32AE 04EBE100 1278B1D2
    52E81B60 C68AA2E8 F84A20BE FE7990EB
    5D44E4B6 16369263 1DDAACBC 280FF19E
    86CF4319 0B8615A8 4FF0512E B123B8EC
    ------ END LICENSE ------
     
    ----- BEGIN LICENSE -----
    Peter Eriksson
    Single User License
    EA7E-890068
    8E107C71 3100D6FC 2AC805BF 9E627C77
    72E710D7 43392469 D06A2F5B F9304FBD
    F5AB4DB2 7A95F172 FE68E300 42745819
    E94AB2DF C1893094 ECABADC8 71FEE764
    20224821 3EABF931 745AF882 87AD0A4B
    33C6E377 0210D712 CD2B1178 82601542
    C7FD8098 F45D2824 BC7DFB38 F1EBD38A
    D7A3AFE0 96F938EA 2D90BD72 9E34CDF0
    ------ END LICENSE ------
     
    ----- BEGIN LICENSE -----
    Ryan Clark
    Single User License
    EA7E-812479
    2158A7DE B690A7A3 8EC04710 006A5EEB
    34E77CA3 9C82C81F 0DB6371B 79704E6F
    93F36655 B031503A 03257CCC 01B20F60
    D304FA8D B1B4F0AF 8A76C7BA 0FA94D55
    56D46BCE 5237A341 CD837F30 4D60772D
    349B1179 A996F826 90CDB73C 24D41245
    FD032C30 AD5E7241 4EAA66ED 167D91FB
    55896B16 EA125C81 F550AF6B A6820916
    ------ END LICENSE ------
 ```
 - 安装`packagecontrol`,
    -  使用快捷键` ctrl+~ ` 或者鼠标依次点击 工具栏 - show console，然后再控制台中贴入以下命令（[详见packagecontrol官网][2]）：
``` subline 
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
 - 安装常用的插件以及设置,
    - 颜色主题选择 `Dawn`
    - 额外的插件安装 `ctrl + shift + p`调出`package control` 点击 `install package` ,然后搜索相关插件

  [1]: http://www.sublimetext.com/3
  [2]: https://packagecontrol.io/installation