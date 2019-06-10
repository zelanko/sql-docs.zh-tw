---
title: 安全性概念
titleSuffix: SQL Server big data clusters
description: 本文說明 SQL Server 2019 巨量資料叢集 （預覽） 的安全性概念。 這包括描述叢集端點和叢集驗證。
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: a71c4fb8902bb016de0d5ee607f955db61d94901
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66783068"
---
# <a name="security-concepts-for-sql-server-big-data-clusters"></a>SQL Server 的巨量資料叢集的安全性概念

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

安全的巨量資料叢集表示一致且協調的支援，驗證和授權的情況下，跨 SQL Server 與 HDFS/Spark。 驗證是確認使用者或服務的身分識別，並確保他們所自稱 」 為人的程序。 授權是指授與或拒絕特定的資源提出要求的使用者身分識別為基礎的存取權。 使用者識別透過驗證之後，會執行此步驟。

在巨量資料內容中的授權通常是透過存取控制清單 (Acl)，其中關聯的特定權限的使用者身分識別執行。 HDFS 支援藉由限制存取服務的 Api、 HDFS 檔案和執行作業的授權。

本文將介紹巨量資料叢集的重要安全性相關概念。

## <a name="cluster-endpoints"></a>叢集端點

有三個蟼檓懘巨量資料叢集

* HDFS/Spark (Knox) 閘道-這是以 HTTPS 為基礎的端點。 其他端點會透過 proxy 進行此程序。 用於存取 webHDFS 等 Livy 服務會使用 HDFS/Spark 閘道。 只要您看到 Knox 的參考，這會是端點。

* 控制器端點會公開 REST Api 來管理叢集的巨量資料叢集管理服務。 某些工具，例如系統管理員入口網站中，也是透過此端點存取。

* 主要執行個體-適用於資料庫工具和應用程式連接到 SQL Server Master 執行個體在叢集中的 TDS 端點。

![叢集端點](media/concept-security/cluster_endpoints.png)

目前沒有開啟用於從外部存取叢集的其他連接埠的任何選項。

### <a name="how-endpoints-are-secured"></a>端點的安全性

保護端點中的巨量資料叢集是使用密碼可以/更新集是使用環境變數或 CLI 命令。 所有的叢集內部的密碼會儲存為 Kubernetes 祕密。  

## <a name="authentication"></a>驗證

時佈建叢集，系統會建立登入數目。

這些登入的一些服務彼此通訊，而其他人的使用者來存取叢集。

### <a name="end-user-authentication"></a>使用者驗證
時佈建叢集，必須使用環境變數設定的使用者密碼數目。 以下是 SQL 系統管理員 」 和 「 叢集管理員用來存取服務的密碼：

控制器的使用者名稱：
 + CONTROLLER_USERNAME=<controller_username>

控制站的密碼：  
 + CONTROLLER_PASSWORD=<controller_password>

SQL Master SA 密碼： 
 + MSSQL_SA_PASSWORD=<controller_sa_password>

密碼存取 HDFS/Spark 端點：
 + KNOX_PASSWORD=<knox_password>

### <a name="intra-cluster-authentication"></a>叢集內驗證

在叢集的部署，會建立 SQL 登入數目：

* 是，使用系統管理員角色管理系統的控制器 SQL 執行個體中建立特殊的 SQL 登入。 此登入的密碼會擷取為 K8s 祕密。

* 控制站擁有及管理叢集中的所有 SQL 執行個體中建立系統管理員登入。 需要執行系統管理工作，例如 HA 安裝或升級，這些執行個體上的控制器。 這些登入也會用於 SQL 執行個體，例如通訊與資料集區的 SQL 主要執行個體之間的叢集間通訊。

> [!NOTE]
> 在目前的版本中，支援僅基本驗證。 更細緻的存取控制，HDFS 物件和 SQL 巨量資料叢集計算和資料集區，尚無法使用。

## <a name="intra-cluster-communication"></a>叢集內通訊

使用憑證來保護與巨量資料叢集，例如 Livy Spark 或儲存體集區中，Spark 內的非 SQL 服務的通訊。 所有的 SQL Server 與 SQL Server 的通訊會受到保護使用 SQL 登入。

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 巨量資料叢集，請參閱下列資源：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
- [研討會：Microsoft SQL Server 的巨量資料叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
