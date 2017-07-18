---
title: "PolyBase 組態 | Microsoft Docs"
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: 17
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 109b5a18604b2111f3344ba216a6d3d98131d116
ms.openlocfilehash: dd9edc9dccf29c21bb37bb0347c8a8cdb87e2b21
ms.contentlocale: zh-tw
ms.lasthandoff: 07/12/2017

---
# <a name="polybase-configuration"></a>PolyBase 設定
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  請使用下列程序來設定 PolyBase。  
  
## <a name="external-data-source-configuration"></a>外部資料來源設定  
 您必須確定可從 SQL Server 連線到外部資料來源。 連線類型能大幅影響查詢效能。 例如，針對 PolyBase 查詢，10Gbit 乙太網路連結將產生比 1Gbit 乙太網路連結更快速的回應時間。  
  
 您必須使用 **sp_configure**設定 SQL Server，以連接到 Hadoop 版本或 Azure Blob 儲存體。 PolyBase 支援兩種 Hadoop 散發：Hortonworks Data Platform (HDP) 和 Cloudera 分散式 Hadoop (CDH)。  如需支援的外部資料來源的完整清單，請參閱 [PolyBase 組態 &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。  
 
 請注意： PolyBase 不支援 Cloudera 加密區域。 
  
### <a name="run-spconfigure"></a>執行 sp_configure  
  
1.  執行 sp_configure ’hadoop connectivity’ 並設定適當的值。  若要尋找值，請參閱 [PolyBase 組態 &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。  
  
    ```tsql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  您必須使用 **services.msc** 重新啟動 SQL Server。 重新啟動 SQL Server 時，會重新啟動下列服務︰  
  
    -   SQL Server PolyBase Data Movement Service  
  
    -   SQL Server PolyBase Engine  
  
## <a name="pushdown-configuration"></a>下推設定  
 若要改善查詢效能，讓計算下推到 Hadoop 叢集，您需要提供 SQL Server 的某些 Hadoop 環境特有的組態參數：  
  
1.  在 SQL Server 的安裝路徑中，尋找 **yarn-site.xml** 檔案。 通常其路徑如下：  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  在 Hadoop 電腦上，尋找 Hadoop 組態目錄中的類比檔案。 在檔案中，尋找並複製組態機碼 yarn.application.classpath 的值。  
  
3.  在 SQL Server 電腦上，尋找 **yarn.site.xml** 檔案中的 **yarn.application.classpath** 屬性。 將 Hadoop 電腦的值貼到 value 元素中。  

4. 針對所有 CDH 5.X 版本，您需要將 **mapreduce.application.classpath** 組態參數新增至 **yarn.site.xml 檔案**結尾或 **mapred-site.xml 檔案**。 HortonWorks 會將這些組態包含在 **yarn.application.classpath** 組態內。

## <a name="example-yarn-sitexml-and-mapred-sitexml-files-for-cdh-5x-cluster"></a>範例 yarn-site.xml 和 mapred-site.xml 檔 CDH 5.X 叢集。



Yarn-site.xml 以 yarn.application.classpath 和 mapreduce.application.classpath 設定。
```
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/,$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>

```
如果您選擇將兩個組態設定分成 mapred-site.xml 和 yarn-site.xml，則檔案會如下所示：

**yarn-site.xml**
```
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>
```

**mapred-site.xml**

請注意，我們已新增 mapreduce.application.classpath 屬性。 在 CDH 5.x 中，您將會在 Ambari 的相同命名慣例下找到組態值。

```
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
  <property>
    <name>mapred.min.split.size</name>
      <value>1073741824</value>
  </property>
  <property>
    <name>mapreduce.app-submission.cross-platform</name>
    <value>true</value>
  </property>
<property>
    <name>mapreduce.application.classpath</name>
    <value>$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH</value>
  </property>


<!--kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
    <name>mapreduce.jobhistory.principal</name>
    <value></value>
  </property>
  <property>
    <name>mapreduce.jobhistory.address</name>
    <value></value>
  </property>
-->
</configuration>
  
```
  
## <a name="kerberos-configuration"></a>Kerberos 設定  
請注意，向 Kerberos 受保護叢集驗證 PolyBase 時，我們需要將 hadoop.rpc.protection 設定設為 authentication。 這會導致 Hadoop 節點之間的資料通訊未加密。 

 連接到由 Kerberos 保護的 Hadoop 叢集 [使用 MIT KDC]：
   
  
1.  在 SQL Server 的安裝路徑中，尋找 Hadoop 組態目錄。 通常其路徑如下：  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  尋找資料表中所列之組態機碼的 Hadoop 端組態值。 (在 Hadoop 電腦上，尋找 Hadoop 組態目錄中的檔案)。  
  
3.  將組態值複製到 SQL Server 電腦上對應檔案中的 Value 屬性。  
  
    |**#**|**組態檔**|**組態機碼**|**動作**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|指定 KDC 主機名稱。 例如：kerberos.your-realm.com。|  
    |2|core-site.xml|polybase.kerberos.realm|指定 Kerberos 領域。 例如：YOUR-REALM.COM|  
    |3|core-site.xml|hadoop.security.authentication|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如：KERBEROS<br></br>**安全性注意事項︰** KERBEROS 必須為大寫。 如果為小寫，KERBEROS 可能不會開啟。|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如： hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如： mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如：10.193.26.174:10020|  
    |7|yarn-site.xml yarn。|yarn.resourcemanager.principal|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如： yarn/_HOST@YOUR-REALM.COM|  
  
4.  建立資料庫範圍的認證物件，以指定每個 Hadoop 使用者的驗證資訊。 請參閱 [PolyBase T-SQL objects](../../relational-databases/polybase/polybase-t-sql-objects.md)(PolyBase T-SQL 物件)。  
  
## <a name="next-steps"></a>後續的步驟  
 [PolyBase T-SQL 物件](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase 連線組態 &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)  
  
  

