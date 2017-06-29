<!--
.. title: 使用 vSphere Web Client 執行 Launch Console 時提示 'The server name could not be resolved'
.. slug: 使用 vSphere Web Client 執行 Launch Console 時提示 'The server name could not be resolved'
.. date: 2015-06-12 16:43:12 UTC+08:00
.. tags: VMware
.. category:
.. link:
.. description:
.. type: text
-->
## 問題描述
使用 vSphere Web Client 執行 Launch Console 時提示 `The server name could not be resolved`

## 問題原因
VMware vCenter Server Appliance 設定了錯誤的 hostname，導致無法透過 DNS 正確解析 vCenter hostname。

## 解決方法
將 vc 的 hostname 設定完整的 FQDN 並產生新的 SSL 憑證

1. 登入 VMware vCener Server Appliance 管理介面 (vCenterIP:5480)
2. 於 Network/hostname 設定完整的 FDQN
3. 將 Admin 的 Certificate regeneration enabled 設為 Yes
4. 將 VMware vCener Server Appliance 重新開機
5. 將 Admin 的 Certificate regeneration enabled 設為 No

如果沒有完成步驟 3~5 來產生新的 SSL 憑證的話，使用 vSphere Web Client 登入時將會出現下列錯誤訊息。

`Failed to connect to VMware Lookup Servicehttps://vCVA_IP_address:7444/lookupservice/sdk - SSL certificate verification failed.`

## 參考資料
[VMware KB2033338](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2033338)
