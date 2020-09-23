---
title: 以 Active Directory 模式管理巨量資料叢集存取
description: 管理巨量資料叢集存取
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ef2df0bec343d73de90a43e411da92530c3c50c8
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790261"
---
# <a name="manage-big-data-cluster-access-in-active-directory-mode"></a>以 Active Directory 模式管理巨量資料叢集存取

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

此文章描述如何新增具有 *bdcUser* 角色，以及在部署期間透過 *clusterUsers* 組態設定提供之角色的新 Active Directory 群組。

>[!IMPORTANT]
>請勿使用此程序新增具有 *bdcAdmin* 角色的新 Active Directory 群組。 Hadoop 元件 (例如 HDFS 與 Spark) 只允許一個 Active Directory 群組作為超級使用者群組，這相當於 BDC 中的 *bdcAdmin* 角色。 若要在部署之後，將具有 *bdcAdmin* 權限的其他 Active Directory 群組授與巨量資料叢集，您必須在部署期間，將其他使用者與群組新增至已命名的群組。 您可以依照相同的程序，更新具有 *bdcUsers* 角色的群組成員資格。

## <a name="two-overarching-roles-in-the-big-data-cluster"></a>巨量資料叢集中的兩個主要角色

您可以在部署設定檔的 [安全性] 區段中提供 Active Directory 群組，作為巨量資料叢集中兩個主要授權角色的一部分：

* `clusterAdmins`:此參數接受一個 Active Directory 群組。 此群組的成員具有 *bdcAdmin* 角色，也就是說，他們會取得整個叢集的系統管理員權限。 這些成員在 SQL Server 中具有「系統管理員」(sysadmin) 權限、在 Hadoop 分散式檔案系統 (HDFS) 與 Spark 中具有「超級使用者」權限，而在控制器中具有「系統管理員」(administrator) 權限。

* `clusterUsers`:這些 Active Directory 群組會對應至 BDC 中的 *bdcUsers* 角色。 他們是一般使用者，在叢集中沒有系統管理員權限。 他們具有登入 SQL Server 主要執行個體的權限，但根據預設，他們沒有物件或資料的權限。 他們是 HDFS 與 Spark 的一般使用者，沒有「超級使用者」權限。 連線到控制器端點時，這些使用者只能查詢端點 (使用 *azdata bdc endpoints list*)。

若要將 *bdcUser* 權限授與其他 Active Directory 群組，而不改變 Active Directory 內的群組成員資格，請完成下列各節中的程序。

## <a name="grant-bdcuser-permissions-to-additional-active-directory-groups"></a>將 *bdcUser* 權限授與其他 Active Directory 群組

### <a name="create-a-login-for-the-active-directory-user-or-group-in-the-sql-server-master-instance"></a>為 SQL Server 主要執行個體中的 Active Directory 使用者或群組建立登入

1. 使用您最愛的 SQL 用戶端連線到主要 SQL 端點。 使用任何系統管理員登入 (例如，在部署期間提供的 `AZDATA_USERNAME`)。 或者，這也可以是屬於 Active Directory 群組的任何 Active Directory 帳戶，該帳戶在安全性設定中以 `clusterAdmins` 的形式提供。

1. 若要建立 Active Directory 使用者或群組的登入，請執行下列 TSQL 命令：

   ```sql
   CREATE LOGIN [<domain>\<principal>] FROM WINDOWS;
   ```

   在 SQL Server 執行個體中授與所需的權限：

   ```sql
   ALTER SERVER ROLE <server role> ADD MEMBER [<domain>\<principal>];
   GO
   ```

如需完整的伺服器角色清單，請參閱[這裡](../relational-databases/security/authentication-access/server-level-roles.md)的對應 SQL Server 安全性主題。

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

1. 使用上述連線，在 *roles* 與 *active_directory_principals* 資料表中插入新的資料列。 以大寫字母輸入 *REALM* 值。

   ```sql
   USE controller;
   GO

   INSERT INTO [controller].[auth].[roles] VALUES (N'<user or group name>@<REALM>', 'bdcUser')
   GO

   INSERT INTO [controller].[auth].[active_directory_principals] VALUES (N'<user or group name>@<REALM>', N'<SID>')
   GO
   ```

   若要尋找要新增之使用者或群組的 SID，您可以使用 [Get-ADUser](/powershell/module/addsadministration/get-aduser/) 或 [Get-ADGroup](/powershell/module/addsadministration/get-adgroup/) PowerShell 命令。

2. 透過登入控制器端點或向 SQL Server 主要執行個體進行驗證，以確認您新增的群組成員具有預期的 *bdcUser* 權限。 例如：

   ```bash
   azdata login
   azdata bdc endpoints list
   ```

## <a name="next-steps"></a>後續步驟

- [SQL Server 2019 巨量資料叢集的安全性概念](concept-security.md)
