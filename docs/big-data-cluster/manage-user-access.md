---
title: 以 Active Directory 模式管理巨量資料叢集存取
description: 管理巨量資料叢集存取
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f9cca7e761b8f8ec3f5b87e9a195a0eb8b5da6d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76259456"
---
# <a name="manage-big-data-cluster-access-in-active-directory-mode"></a>以 Active Directory 模式管理巨量資料叢集存取

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

此文章說明如何更新 clusterAdmins 與 clusterUsers 部署期間所提供的 Active Directory 群組。

## <a name="two-overarching-roles-in-the-big-data-cluster"></a>巨量資料叢集中的兩個主要角色

您可以在部署設定檔的 [安全性] 區段中提供 Active Directory 群組，作為巨量資料叢集中兩個主要授權角色的一部分：

* `clusterAdmins`:此參數接受一個 Active Directory 群組。 此群組的成員會取得整個叢集的系統管理員權限。 這些成員在 SQL Server 中具有「系統管理員」(sysadmin)  權限、在 Hadoop 分散式檔案系統 (HDFS) 與 Spark 中具有「超級使用者」  權限，而在控制器中具有「系統管理員」(administrator)  權限。

* `clusterUsers`:這些 Active Directory 群組是一般使用者，在叢集中沒有系統管理員權限。 他們具有登入 SQL Server 主要執行個體的權限，但根據預設，他們沒有物件或資料的權限。

在部署之後，將其他 Active Directory 群組權限授與巨量資料叢集的其中一種方式，就是在部署期間，將其他使用者與群組新增至已命名的群組。 

不過，要求系統管理員改變 Active Directory 內的群組成員資格或許不可行。 若要授與其他 Active Directory 群組權限，而不改變 Active Directory 內的群組成員資格，請完成下一節中的程序。

## <a name="grant-administrator-permissions-to-additional-active-directory-groups"></a>將管理員權限授與其他 Active Directory 群組

>[!IMPORTANT]
>此程序不會將其他 Active Directory 群組管理員存取權授與巨量資料叢集中的 Hadoop 元件 (例如 HDFS 與 Spark)。 這些元件僅允許一個 Active Directory 群組作為超級使用者群組。 此限制表示即使在此步驟之後，部署期間在 `clusterAdmins` 中指定的群組仍會維持超級使用者群組。

遵循此節中的程序，您可以同時將系統管理員存取權授與控制器和 SQL Server 主要執行個體。

### <a name="create-a-login-for-the-active-directory-user-or-group-in-the-sql-server-master-instance"></a>為 SQL Server 主要執行個體中的 Active Directory 使用者或群組建立登入 

1. 使用您最愛的 SQL 用戶端連線到主要 SQL 端點。 使用任何系統管理員登入 (例如，在部署期間提供的 `AZDATA_USERNAME`)。 或者，這也可以是屬於 Active Directory 群組的任何 Active Directory 帳戶，該帳戶在安全性設定中以 `clusterAdmins` 的形式提供。

1. 若要建立 Active Directory 使用者或群組的登入，請執行下列 TSQL 命令：

   ```sql
   CREATE LOGIN [<domain>\<principal>] FROM WINDOWS;
   ```

   若要在 SQL Server 執行個體中授與系統管理員權限，也請授與下列權限：

   ```sql
   ALTER SERVER ROLE sysadmin ADD MEMBER [<domain>\<principal>];
   GO
   ```

### <a name="add-the-active-directory-user-or-group-to-the-roles-table-in-the-controller-database"></a>將 Active Directory 使用者或群組新增至控制器資料庫中的角色資料表 

1. 透過執行下列命令來取得控制器 SQL Server 認證：

   a. 以 Kubernetes 系統管理員身分執行此命令：

   ```bash
   kubectl get secret controller-sa-secret -n <cluster name> -o yaml | grep password
   ```

   b. 以 Base64 方式將祕密解碼：

   ```bash
   echo <password from kubectl command>  | base64 --decode && echo
   ```

1. 在個別的命令視窗中，公開控制器資料庫伺服器連接埠：

   ```bash
   kubectl port-forward controldb-0 1433:1433 --address 0.0.0.0 -n <cluster name>
   ```

1. 使用上述連線，在角色資料表中插入資料列。 以大寫字母輸入 *REALM* 值。

   如果您要授與系統管理員權限，請使用 *\<角色名稱>* 中的 *bdcAdmin* 角色。 針對非系統管理員使用者，請使用 *bdcUser* 角色。

   ```sql
   USE controller;
   GO

   INSERT INTO [controller].[auth].[roles] VALUES (N'<user or group name>@<REALM>', N'<role name>')
   GO
   ```

1. 透過登入控制器端點並執行下列命令，確認您新增的群組成員具有巨量資料叢集系統管理員權限：

   ```bash
   azdata bdc config show
   ```

1. 針對非系統管理員使用者，您可以透過使用 `azdata login` 向 SQL 主要執行個體或向控制器驗證以確認存取權。

## <a name="next-steps"></a>後續步驟

- [SQL Server 2019 巨量資料叢集的安全性概念](concept-security.md)
