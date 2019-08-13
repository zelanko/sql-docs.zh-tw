---
title: 安全性概念
titleSuffix: SQL Server big data clusters
description: 本文描述 SQL Server 2019 巨量資料叢集 (預覽) 的安全性概念。 其中包括叢集端點和叢集驗證的說明。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 54ae86785590eb26fb8ac402f3ae8ab6c7f29a98
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958669"
---
# <a name="security-concepts-for-sql-server-big-data-clusters"></a>SQL Server 巨量資料叢集的安全性概念

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

安全的巨量資料叢集是指在 SQL Server 與 HDFS/Spark 之間，針對驗證和授權案例提供一致且連貫的支援。 驗證是驗證使用者或服務識別的程序，並確保其為所宣稱的身分。 授權是指根據要求使用者的識別，授與或拒絕對特定資源的存取。 此步驟是在透過驗證識別使用者之後執行。

巨量資料內容中的授權通常是透過存取控制清單 (ACL) 執行，這會建立使用者識別與特定權限的關聯。 HDFS 藉由限制對服務 API、HDFS 檔案和作業執行的存取來支援授權。

本文將涵蓋巨量資料叢集中與安全性相關的重要概念。

## <a name="cluster-endpoints"></a>叢集端點

巨量資料叢集有三個進入點

* HDFS/Spark (Knox) 閘道 - 這是 HTTPS 式的端點。 其他端點則是透過此端點來代理。 HDFS/Spark 閘道可用於存取 webHDFS 和 Livy 等服務。 無論您在何處看到 Knox 的參考，這就是端點。

* 控制器端點 - 公開 REST API 來管理叢集的巨量資料叢集管理服務。 某些工具也會透過此端點存取。

* 主要執行個體 - 用來連線到叢集中 SQL Server 主要執行個體的資料庫工具和應用程式 TDS 端點。

![叢集端點](media/concept-security/cluster_endpoints.png)

目前沒有開啟其他連接埠從外部存取叢集的選項。

### <a name="how-endpoints-are-secured"></a>如何保護端點

巨量資料叢集中的端點是使用密碼保護，可透過環境變數或 CLI 命令進行設定/更新。 所有叢集內部密碼都會儲存為 Kubernetes 祕密。  

## <a name="authentication"></a>驗證

佈建叢集之後，會建立數個登入。

有些登入是為了讓服務能彼此通訊，其他登入是為了讓終端使用者存取叢集。

### <a name="end-user-authentication"></a>終端使用者驗證
佈建叢集之後，必須使用環境變數設定數個終端使用者密碼。 這些是 SQL 系統管理員和叢集管理員用來存取服務的密碼：

控制器使用者名稱：
 + CONTROLLER_USERNAME=<controller_username>

控制器密碼：  
 + CONTROLLER_PASSWORD=<controller_password>

SQL 主要 SA 密碼： 
 + MSSQL_SA_PASSWORD=<controller_sa_password>

用於存取 HDFS/Spark 端點的密碼：
 + KNOX_PASSWORD=<knox_password>

### <a name="intra-cluster-authentication"></a>叢集內驗證

部署叢集之後，會建立數個 SQL 登入：

* 在控制器 SQL 執行個體中，建立由系統管理並具有系統管理員角色的特殊 SQL 登入。 此登入的密碼會以 K8s 祕密形式擷取。

* 在叢集的所有 SQL 執行個體中，建立由控制器擁有和管理的系統管理員登入。 控制器需要此登入，才能在這些執行個體上執行管理工作 (例如 HA 安裝或升級)。 這些登入也可用於 SQL 執行個體之間的叢集內通訊，例如與資料集區通訊的 SQL 主要執行個體。

> [!NOTE]
> 在目前版本中，僅支援基本驗證。 目前還無法對 HDFS 物件以及 SQL 巨量資料叢集計算和資料集區進行精細存取控制。

## <a name="intra-cluster-communication"></a>叢集內通訊

與巨量資料叢集內的非 SQL 服務通訊 (例如 Livy 對 Spark 或 Spark 對存放集區) 是使用憑證保護。 所有 SQL Server 對 SQL Server 的通訊是使用 SQL 登入保護。

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 巨量資料叢集，請參閱下列資源：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
- [工作坊：Microsoft SQL Server 巨量資料叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
