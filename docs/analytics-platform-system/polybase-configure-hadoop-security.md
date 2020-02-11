---
title: 設定 PolyBase Hadoop 安全性
description: 說明如何在平行處理資料倉儲中設定 PolyBase，以連線至外部 Hadoop。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/26/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f275c77556e8abe8932e241075b9e24e2ae5db77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400660"
---
# <a name="polybase-configuration-and-security-for-hadoop"></a>Hadoop 的 PolyBase 設定和安全性

本文提供各種設定的參考，這些設定會影響連線到 Hadoop 的 AP PolyBase。 如需 PolyBase 的相關逐步解說，請參閱[什麼是 polybase](configure-polybase-connectivity-to-external-data.md)。

> [!NOTE]
> 在 AP 上，所有計算節點和控制節點上都需要 XML 檔案的變更。
> 
> 修改 AP 中的 XML 檔案時，請特別小心。 任何遺漏的標記或不想要的字元，都會使 xml 檔案失效，而阻礙此功能的 usablilty。
> Hadoop 設定檔位於下列路徑：  
> ```  
> C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf 
> ``` 
> 對 xml 檔案所做的任何變更都需要重新開機服務，才會生效。

## <a id="rpcprotection"></a> Hadoop.RPC.Protection 設定

hadoop 叢集中保護通訊的常見方式，是將 hadoop.rpc.protection 組態變更為「私人」或「完整性」。 根據預設，PolyBase 假設設定是設定為「驗證」。 若要覆寫此預設值，請將下列屬性新增至 core-site.xml 檔案。 變更此設定可保護 Hadoop 節點之間的資料傳輸以及與 SQL Server 的 SSL 連線。

```xml
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
   <property>
     <name>hadoop.rpc.protection</name>
     <value></value>
   </property> 
```

## <a id="kerberossettings"></a>Kerberos 設定  

請注意，根據預設，向 Kerberos 受保護叢集驗證 PolyBase 時，需要 hadoop.rpc.protection 設定為「驗證」。 這會導致 Hadoop 節點之間的資料通訊未加密。 若要使用 hadoop.rpc.protection 的「隱私權」或「完整性」設定，請更新 PolyBase 伺服器上的 core-site.xml 檔案。 如需詳細資訊，請參閱上一節：[連線至 Hadoop 叢集與 Hadoop.rpc.protection](#rpcprotection)。

若要使用 MIT KDC 連接到受 Kerberos 保護的 Hadoop 叢集，所有 AP 計算節點和控制節點都需要下列變更：

1. 在 [AP] 的安裝路徑中尋找 Hadoop 設定目錄。 通常其路徑如下：  

   ```  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf  
   ```  

2. 尋找資料表中所列之組態機碼的 Hadoop 端組態值。 (在 Hadoop 電腦上，尋找 Hadoop 組態目錄中的檔案)。  
   
3. 將組態值複製到 SQL Server 電腦上對應檔案中的 Value 屬性。  
   
   |**#**|**組態檔**|**組態機碼**|**動作**|  
   |------------|----------------|---------------------|----------|   
   |1|core-site.xml|polybase.kerberos.kdchost|指定 KDC 主機名稱。 例如：kerberos.your-realm.com。|  
   |2|core-site.xml|polybase.kerberos.realm|指定 Kerberos 領域。 例如：YOUR-REALM.COM|  
   |3|core-site.xml|hadoop.security.authentication|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如：KERBEROS<br></br>**安全性注意事項︰** KERBEROS 必須為大寫。 如果為小寫，KERBEROS 可能不會開啟。|   
   |4|hdfs-site.xml|dfs.namenode.kerberos.principal|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如： hdfs/_HOST@YOUR-REALM.COM|  
   |5|mapred-site.xml|mapreduce.jobhistory.principal|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如： mapred/_HOST@YOUR-REALM.COM|  
   |6|mapred-site.xml|mapreduce.jobhistory.address|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如：10.193.26.174:10020|  
   |7|yarn-site.xml yarn。|yarn.resourcemanager.principal|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如： yarn/_HOST@YOUR-REALM.COM|  

**core-site.xml**
```xml
<property>
  <name>polybase.kerberos.realm</name>
  <value></value>
</property>
<property>
  <name>polybase.kerberos.kdchost</name>
  <value></value>
</property>
<property>
    <name>hadoop.security.authentication</name>
    <value>KERBEROS</value>
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.namenode.kerberos.principal</name>
  <value></value> 
</property>
```

**mapred-site.xml**
```xml
<property>
  <name>mapreduce.jobhistory.principal</name>
  <value></value>
</property>
<property>
  <name>mapreduce.jobhistory.address</name>
  <value></value>
</property>
```

**yarn-site.xml**
```xml
<property>
  <name>yarn.resourcemanager.principal</name>
  <value></value>
</property>
```

4. 建立資料庫範圍的認證物件，以指定每個 Hadoop 使用者的驗證資訊。 請參閱 [PolyBase T-SQL objects](../relational-databases/polybase/polybase-t-sql-objects.md)(PolyBase T-SQL 物件)。

## <a id="encryptionzone"></a>Hadoop 加密區域設定
如果您使用 Hadoop 加密區域，請修改 core-site.xml 和 hdfs-site.xml，如下所示。 提供 KMS 服務執行時使用對應埠號碼的 ip 位址。 CDH 上的 KMS 預設埠是16000。

**core-site.xml**
```xml
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value> 
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.encryption.key.provider.uri</name>
  <value>kms://http@<ip address>:16000/kms</value>
</property>
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value>
  </property>
```