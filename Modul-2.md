---
layout: page
title: Modul 2
parent: Modul
permalink: /modul/modul-2/
---

## Perubahan File Konfigurasi dari Open5GS EPC dan srsRAN 4G ZMQ UE / RAN
konfigurasinya gimana, apa aja, jelasin lebih dalem

## Konfigurasi Core Network (EPC) pada Open5GS
### Control Plane
#### mme.yaml
`/etc/open5gs/mme.yaml`
```diff
--- mme.yaml.orig       2024-10-27 08:48:52.000000000 +0900
+++ mme.yaml    2024-11-09 00:50:59.006621937 +0900
@@ -12,7 +12,7 @@
   freeDiameter: /root/open5gs/install/etc/freeDiameter/mme.conf
   s1ap:
     server:
-      - address: 127.0.0.2
+      - address: 192.168.0.111
   gtpc:
     server:
       - address: 127.0.0.2
@@ -27,14 +27,14 @@
         port: 9090
   gummei:
     - plmn_id:
-        mcc: 999
-        mnc: 70
+        mcc: 001
+        mnc: 01
       mme_gid: 2
       mme_code: 1
   tai:
     - plmn_id:
-        mcc: 999
-        mnc: 70
+        mcc: 001
+        mnc: 01
       tac: 1
   security:
     integrity_order : [ EIA2, EIA1, EIA0 ]
```
