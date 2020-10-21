---
title: Active Directory 物件
titleSuffix: SQL Server Big Data Cluster
description: 描述針對 SQL Server巨量資料叢集所建立的 Active Directory 物件。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fcd045c07e7300478e811b2bbc4b9a0f5dfaab52
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892448"
---
# <a name="auto-generated-active-directory-objects"></a>已自動產生 Active Directory 物件

本文描述 SQL Server 在巨量資料叢集 (BDC) 部署期間所建立的 Active Directory (AD) 帳戶和群組。

## <a name="accounts--groups"></a>帳戶與群組

在叢集部署期間，在所提供[組織單位 (OU)](/windows-server/identity/ad-ds/plan/reviewing-ou-design-concepts) 中產生的使用者帳戶和群組。

每個帳戶都代表 BDC 中的一項服務。 這些帳戶擁有每項服務所需的服務主體名稱 (SPN)。 您可使用 [setspn](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spn-setspn-syntax.aspx) 命令來列出每個帳戶所擁有的 SPN。

部署會自動產生帳戶和群組名稱。 從 SQL Server 2019 CU5 開始，帳戶或群組名稱前置詞就是部署命名空間名稱 (BDC 叢集名稱)。 如果本文的項目叢集名稱是 `bdc`，請使用 `bdc` 取代 `<prefix>` 以識別帳戶。

Pod 尾碼 (-x) 代表下面的變數 Pod 識別碼。 以下名稱不包含使用者在部署期間提供的變數前置詞。

傳統帳戶名稱適用於使用 SQL Server 2019 CU5 以前版本的部署，以及在安全性組態中，將 "useSubdomain" 選項設為 false 所完成的部署。

| 帳戶或群組名稱|詳細資訊|
|----|---|
|`<prefix>-ctrl`|[控制器服務帳戶](#controller-service-account)|
|`<prefix>-ngxm`|[監視服務 Proxy 服務帳戶](#monitoring-service-proxy-service-account)|
|`<prefix>-ldap`|[LDAP 查閱使用者](#ldap-lookup-user)|
|`<prefix>-sqc0-x/<prefix>-sqc0`|[計算集區 SQL Server 使用者](#compute-pool-sql-server-user)|
|`<prefix>-dmc0-x`|[計算集區資料倉儲 DMS 使用者](#compute-pool-data-warehouse-dms-user)|
|`<prefix>-dec0-x`|[計算集區資料倉儲引擎使用者](#compute-pool-data-warehouse-engine-user)|
|`<prefix>-sqd0`|[計算集區 SQL Server 使用者](#data-pool-sql-server-user)|
|`<prefix>-sqs0`|[儲存集區 SQL Server 使用者](#storage-pool-sql-server-user)|
|`<prefix>-ynt0-x`|[儲存集區 Yarn 節點管理員服務使用者](#storage-pool-yarn-node-manager-service-user)|
|`<prefix>-htt0`|[儲存集區 HTTP 服務使用者](#storage-pool-http-service-user)|
|`<prefix>-hdt0`|[儲存集區 HDFS datanode 服務使用者](#storage-pool-hdfs-datanode-service-user)|
|`<prefix>-hdnn`|[HDFS 名稱節點服務使用者](#hdfs-name-node-service-user)|
|`<prefix>-htnn`|[HDFS 名稱節點 HTTP 服務使用者](#hdfs-name-node-http-service-user)|
|`<prefix>-kmnn-x`|[名稱節點 KMS 服務使用者](#name-node-kms-service-user)|
|`<prefix>-jnzk-x`|[Zookeeper JournalNode 服務使用者](#zookeeper-journalnode-service-users)|
|`<prefix>-htzk`|[Zookeeper HTTP 服務使用者](#zookeeper-http-service-user)|
|`<prefix>-yrsh-x`|[Sparkhead Yarn 資源管理員服務使用者](#sparkhead-yarn-resource-manager-service-user)|
|`<prefix>-htsh`|[Sparkhead HTTP 使用者](#sparkhead-http-user)|
|`<prefix>-shsh-x`|[Sparkhead Spark 歷程記錄服務使用者](#sparkhead-spark-history-service-user)|
|`<prefix>-lvsh-x`|[Sparkhead Livy 服務使用者](#sparkhead-livy-service-user)|
|`<prefix>-hvsh-x`|[Sparkhead Hive 服務使用者](#sparkhead-hive-service-user)|
|`<prefix>-yns0-x`|[Spark 集區 Yarn 節點管理員服務使用者](#spark-pool-yarn-node-manager-service-user)|
|`<prefix>-hts0`|[Spark 集區 Yarn 節點管理員 HTTP 使用者](#spark-pool-yarn-node-manager-http-user)|
|`<prefix>-knox-x`|[Knox 閘道使用者](#knox-gateway-user)|
|`<prefix>-htgw`|[Knox 閘道 HTTP 使用者](#knox-gateway-http-user)|
|`<prefix>-apst`|[應用程式設定使用者](#app-setup-user)|
|`<prefix>-dmsvc`|[資料倉儲 DMS 服務群組](#data-warehouse-dms-service-group)|
|`<prefix>-desvc`|[資料倉儲引擎服務群組](#data-warehouse-engine-service-group)|

下一節會詳述每個帳戶。 如需群組的相關資訊，請跳至[群組](#groups)。

## <a name="controller-management--ldap-related-accounts"></a>控制器、管理與 LDAP 相關帳戶

### <a name="controller-service-account"></a>控制器服務帳戶

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`control`|
|Pod 名稱|`control-x`|
|容器名稱|`controller`|
|服務名稱|`controller`|
|帳戶名稱 (不含前置詞)| `ctrl`|
|帳戶 (具有命名空間前置詞)|`<prefix>-ctrl`|
|傳統帳戶名稱|`ctrl-controller`|

### <a name="monitoring-service-proxy-service-account"></a>監視服務 Proxy 服務帳戶

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`mgmtproxy`|
|Pod 名稱|`mgmtproxy-x`|
|容器名稱|`service-proxy`|
|服務名稱|`nginx`|
|帳戶 (不含前置詞)| `ngxm`|
|帳戶 (具有命名空間前置詞)|`<prefix>-ngxm`|
|傳統帳戶名稱|`nginx-mgmtproxy`|

### <a name="ldap-lookup-user"></a>LDAP 查閱使用者

供 grafana 和 hadoop 服務使用，以透過 LDAP 查閱使用者。

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`metricsui`|
|Pod 名稱|`metricsui-x`|
|容器名稱|`grafana`|
|服務名稱|`grafana`|
|帳戶名稱 (不含前置詞)| `ldap`|
|帳戶名稱 (具有命名空間前置詞)|`<prefix>-ldap`|
|傳統帳戶名稱|`ldap-user`|

## <a name="master-pool-accounts"></a>主要集區帳戶

### <a name="master-pool-sql-server-user"></a>主要集區 SQL Server 使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`master`|
|Pod 名稱|`master-x`|
|容器名稱|`mssql-server`|
|服務名稱|`mssql`|
|帳戶名稱 (不含前置詞)| `sqmp-x/sqmp`|
|帳戶名稱 (具有命名空間前置詞)|`<prefix>-sqmp-x/<prefix>-sqmp`|
|傳統帳戶名稱|`mssql-master-x`|

### <a name="master-pool-data-warehouse-dms-user"></a>主要集區資料倉儲 DMS 使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`master`|
|Pod 名稱|`master-x`|
|容器名稱|`mssql-server`|
|服務名稱|`dwdms`|
|帳戶 (不含前置詞)| `dmmp-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-dmmp-x`|
|傳統帳戶名稱|`dwdms-master-x`|

### <a name="master-pool-data-warehouse-engine-user"></a>主要集區資料倉儲引擎使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`master`|
|Pod 名稱|`master-x`|
|容器名稱|`mssql-server`|
|服務名稱|`dweng`|
|帳戶 (不含前置詞)| `demp`|
|帳戶 (具有命名空間前置詞)|`<prefix>-demp-x`|
|傳統帳戶名稱|`dweng-master-x`|

## <a name="compute-pool-accounts"></a>計算集區帳戶

### <a name="compute-pool-sql-server-user"></a>計算集區 SQL Server 使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`compute-0`|
|Pod 名稱|`compute-0-x`|
|容器名稱|`mssql-server`|
|服務名稱|`mssql`|
|帳戶 (不含前置詞)| `sqc0-x/sqlc0`|
|帳戶 (具有命名空間前置詞)|`<prefix>-sqc0-x/<prefix>-sqc0`|
|傳統帳戶名稱|`mssql-compute-0-x`|

### <a name="compute-pool-data-warehouse-dms-user"></a>計算集區資料倉儲 DMS 使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`compute-0`|
|Pod 名稱|`compute-0-x`|
|容器名稱|`mssql-server`|
|服務名稱|`dwdms`|
|帳戶 (不含前置詞)| `dmc0-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-dmc0-x`|
|傳統帳戶名稱|`dwdms-compute-0-x`|

### <a name="compute-pool-data-warehouse-engine-user"></a>計算集區資料倉儲引擎使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`compute-0`|
|Pod 名稱|`compute-0-x`|
|容器名稱|`mssql-server`|
|服務名稱|`dweng`|
|帳戶 (不含前置詞)| `dec0-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-dec0-x`|
|傳統帳戶名稱|`dweng-compute-0-x`|

## <a name="data-pool-accounts"></a>資料集區帳戶

### <a name="data-pool-sql-server-user"></a>資料集區 SQL Server 使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`data-0`|
|Pod 名稱|`data-0-x`|
|容器名稱|`mssql-server`|
|服務名稱|`mssql`|
|帳戶 (不含前置詞)| `sqd0`|
|帳戶 (具有命名空間前置詞)|`<prefix>-sqd0`|
|傳統帳戶名稱|`mssql-data-0`|

## <a name="storage-pool-accounts"></a>儲存集區帳戶

### <a name="storage-pool-sql-server-user"></a>儲存集區 SQL Server 使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`storage-0`|
|Pod 名稱|`storage-0-x`|
|容器名稱|`mssql-server`|
|服務名稱|`mssql`|
|帳戶 (不含前置詞)| `sqs0`|
|帳戶 (具有命名空間前置詞)|`<prefix>-sqs0`|
|傳統帳戶名稱|`mssql-storage-0`|

### <a name="storage-pool-yarn-node-manager-service-user"></a>儲存集區 Yarn 節點管理員服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`storage-0`|
|Pod 名稱|`storage-0-x`|
|容器名稱|`hadoop`|
|服務名稱|`Yarn Node Manager`|
|帳戶 (不含前置詞)| `ynt0-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-ynt0-x`|
|傳統帳戶名稱|`yarnnm-storage-0-x`|

### <a name="storage-pool-http-service-user"></a>儲存集區 HTTP 服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`storage-0`|
|Pod 名稱|`storage-0-x`|
|容器名稱|`hadoop`|
|服務名稱|`HDFS Datanode`|
|帳戶 (不含前置詞)| `hdt0`|
|帳戶 (具有命名空間前置詞)|`<prefix>-hdt0`|
|傳統帳戶名稱|`http-storage-0`|

### <a name="storage-pool-hdfs-datanode-service-user"></a>儲存集區 HDFS datanode 服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`storage-0`|
|Pod 名稱|`storage-0-x`|
|容器名稱|`hadoop`|
|服務名稱|`HDFS Datanode`|
|帳戶 (不含前置詞)| `hdt0`|
|帳戶 (具有命名空間前置詞)|`<prefix>-hdt0`|
|傳統帳戶名稱|`hdfsdn-storage-0`|

## <a name="hdfs-accounts"></a>HDFS 帳戶

### <a name="hdfs-name-node-service-user"></a>HDFS 名稱節點服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`nmnode-0`|
|Pod 名稱|`nmnode-0-x`|
|容器名稱|`hadoop`|
|服務名稱|`HDFS Namenode`|
|帳戶 (不含前置詞)| `hdnn`|
|帳戶 (具有命名空間前置詞)|`<prefix>-hdnn`|
|傳統帳戶名稱|`hdfsnn-nmnode`|

### <a name="hdfs-name-node-http-service-user"></a>HDFS 名稱節點 HTTP 服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`nmnode-0`|
|Pod 名稱|`nmnode-0-x`|
|容器名稱|`hadoop`|
|服務名稱|`HDFS Namenode`|
|帳戶 (不含前置詞)| `htnn`|
|帳戶 (具有命名空間前置詞)|`<prefix>-htnn`|
|傳統帳戶名稱|`http-nmnode`|

## <a name="kms-accounts"></a>KMS 帳戶

### <a name="name-node-kms-service-user"></a>名稱節點 KMS 服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`nmnode-0`|
|Pod 名稱|`nmnode-0-x`|
|容器名稱|`hadoop`|
|服務名稱|`KMS`|
|帳戶 (不含前置詞)| `kmnn-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-kmnn-x`|
|傳統帳戶名稱|`kms-nmnode-x`|

## <a name="zookeeper-accounts"></a>Zookeeper 帳戶

### <a name="zookeeper-journalnode-service-users"></a>Zookeeper JournalNode 服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`zookeeper`|
|Pod 名稱|`zookeeper-x`|
|容器名稱|`zookeeper`|
|服務名稱|`Journal node`|
|帳戶 (不含前置詞)| `jnzk-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-jnzk-x`|
|傳統帳戶名稱|`jn-zookeeper-x`|

### <a name="zookeeper-http-service-user"></a>Zookeeper HTTP 服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`zookeeper`|
|Pod 名稱|`zookeeper-x`|
|容器名稱|`zookeeper`|
|服務名稱|`Zookeeper`|
|帳戶 (不含前置詞)| `htzk`|
|帳戶 (具有命名空間前置詞)|`<prefix>-htzk`|
|傳統帳戶名稱|`http-zookeeper`|

## <a name="spark-related-accounts"></a>Spark 相關帳戶

### <a name="sparkhead-yarn-resource-manager-service-user"></a>Sparkhead Yarn 資源管理員服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`sparkhead`|
|Pod 名稱|`sparkhead-x`|
|容器名稱|`hadoop-yarn-jobhistory`|
|服務名稱|`Yarn Resource Manager`|
|帳戶 (不含前置詞)| `yrsh-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-yrsh-x`|
|傳統帳戶名稱|`yarnrm-sparkhead-x`|

### <a name="sparkhead-http-user"></a>Sparkhead HTTP 使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`sparkhead`|
|Pod 名稱|`sparkhead-x`|
|容器名稱|`*`|
|服務名稱|`*`|
|帳戶 (不含前置詞)| `htsh`|
|帳戶 (具有命名空間前置詞)|`<prefix>-htsh`|
|傳統帳戶名稱|`http-sparkhead`|

### <a name="sparkhead-spark-history-service-user"></a>Sparkhead Spark 歷程記錄服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`sparkhead`|
|Pod 名稱|`sparkhead-x`|
|容器名稱|`hadoop-livy-sparkhistory`|
|服務名稱|`Spark History Server`|
|帳戶 (不含前置詞)| `shsh-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-shsh-x`|
|傳統帳戶名稱|`sph-sparkhead-x`|

### <a name="sparkhead-livy-service-user"></a>Sparkhead Livy 服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`sparkhead`|
|Pod 名稱|`sparkhead-x`|
|容器名稱|`hadoop-livy-sparkhistory`|
|服務名稱|`Livy`|
|帳戶 (不含前置詞)| `lvsh-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-lvsh-x`|
|傳統帳戶名稱|`livy-sparkhead-x`|

### <a name="sparkhead-hive-service-user"></a>Sparkhead Hive 服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`sparkhead`|
|Pod 名稱|`sparkhead-x`|
|容器名稱|`hadoop-hivemetastore`|
|服務名稱|`Hive Metastore`|
|帳戶 (不含前置詞)| `hvsh-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-hvsh-x`|
|傳統帳戶名稱|`hive-sparkhead-x`|

### <a name="spark-pool-yarn-node-manager-service-user"></a>Spark 集區 Yarn 節點管理員服務使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`spark-0`|
|Pod 名稱|`spark-0-x`|
|容器名稱|`hadoop`|
|服務名稱|`Yarn Node Manager`|
|帳戶 (不含前置詞)| `yns0-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-yns0-x`|
|傳統帳戶名稱|`yarnnm-spark-0-x`|

### <a name="spark-pool-yarn-node-manager-http-user"></a>Spark 集區 Yarn 節點管理員 HTTP 使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`spark-0`|
|Pod 名稱|`spark-0-x`|
|容器名稱|`hadoop`|
|服務名稱|`Yarn Node Manager`|
|帳戶 (不含前置詞)| `hts0`|
|帳戶 (具有命名空間前置詞)|`<prefix>-hts0`|
|傳統帳戶名稱|`http-spark-0`|

## <a name="knox-accounts"></a>Knox 帳戶

### <a name="knox-gateway-user"></a>Knox 閘道使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`gateway`|
|Pod 名稱|`gateway-x`|
|容器名稱|`knox`|
|服務名稱|`Knox`|
|帳戶 (不含前置詞)| `knox-x`|
|帳戶 (具有命名空間前置詞)|`<prefix>-knox-x`|
|傳統帳戶名稱|`knox-gateway-x`|

### <a name="knox-gateway-http-user"></a>Knox 閘道 HTTP 使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`gateway`|
|Pod 名稱|`gateway-x`|
|容器名稱|`knox`|
|服務名稱|`Knox`|
|帳戶 (不含前置詞)| `htgw`|
|帳戶 (具有命名空間前置詞)|`<prefix>-htgw`|
|傳統帳戶名稱|`http-gateway`|

## <a name="app-accounts"></a>應用程式帳戶

### <a name="app-setup-user"></a>應用程式設定使用者

|Object|帳戶名稱|
|---|---|
|擴展集名稱|`appproxy`|
|Pod 名稱|`appproxy-x`|
|容器名稱|`App Service Proxy`|
|服務名稱|`nginx`|
|帳戶 (不含前置詞)| `apst`|
|帳戶 (具有命名空間前置詞)|`<prefix>-apst`|
|傳統帳戶名稱|`app-setup`|

## <a name="groups"></a>群組

下列群組會建立在使用者所提供的 OU 中。 群組的成員是針對上述對應服務所建立使用者。

### <a name="data-warehouse-dms-service-group"></a>資料倉儲 DMS 服務群組

|Object|群組名稱|
|---|---|
|擴展集名稱|`master/compute-0`|
|Pod 名稱|`master-x/compute-0-x`|
|容器名稱|`mssql-server`|
|服務名稱|`dwdms`|
|群組 (不含前置詞)| `dmsvc`|
|帳戶 (具有命名空間前置詞)|`<prefix>-dmsvc`|
|傳統帳戶名稱|`dwdms-service`|

### <a name="data-warehouse-engine-service-group"></a>資料倉儲引擎服務群組

|Object|群組名稱|
|---|---|
|擴展集名稱|`master/compute-0`|
|Pod 名稱|`master-x/compute-0-x`|
|容器名稱|`mssql-server`|
|服務名稱|`dweng`|
|群組 (不含前置詞)| `desvc`|
|帳戶 (具有命名空間前置詞)|`<prefix>-desvc`|
|傳統帳戶名稱|`desvc`|

## <a name="next-steps"></a>後續步驟

[在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-deploy.md)

[在相同的 Active Directory 網域中部署多個 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](active-directory-deployment-background.md)
