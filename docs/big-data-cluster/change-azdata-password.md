---
title: 更新 AZDATA_PASSWORD
description: 手動更新 `AZDATA_PASSWORD`
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/19/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a3121351fce1ef6c86575789cee5dbb2860ce3c9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728812"
---
# <a name="manually-update-azdata_password"></a>手動更新 `AZDATA_PASSWORD`

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

無論叢集是否使用 Active Directory 整合來運作，`AZDATA_PASSWORD` 都是在部署期間設定。 其提供叢集控制器與主要執行個體的基本驗證。 此文件說明如何手動更新 `AZDATA_PASSWORD`。

## <a name="change-azdata_password-for-controller"></a>變更控制器的 `AZDATA_PASSWORD`

如果叢集是以非 Active Directory 模式運作，請透過執行下列動作來更新 Apache Knox 閘道密碼：

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
 
1. 使用您剛取得的系統管理員密碼，從 SQL 用戶端工具連接到控制器資料庫伺服器。

1. 為 `AZDATA_USERNAME` 產生新的複雜密碼，以取代現有的 `AZDATA_PASSWORD`。

   為了簡化範例，接下來的步驟會使用 "newPassword"，因為產生的密碼為 "newPassword"。 

1. 從使用者資料表取得 `hexsalt`：

   ```sql
   SELECT hexsalt FROM [auth].[users] WHERE username = '<username>'
   ```

   `hexsalt` 會傳回隨機的十六進位字串 (例如，`64FC59DF31244FFEE02F457BC0750226`)。

1. 使用 `hexsalt` 加密新的複雜密碼：

   為了方便起見，我們提供預先建立的工具 `pbkdf2` 來加密密碼。 下載適用於 [`pbkdf2`](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/security/password-hashing/pbkdf2/prebuilt-binaries) 的平台適當 .NET Core 應用程式。

   應用程式是獨立的，而且不需要任何先決條件，例如 .NET 執行階段。 若要加密密碼，請執行：

   ```bash
   pbkdf2 <password> <hexsalt>
   J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=
   ```

1. 更新使用者資料表中的密碼：

   ```SQL
   UPDATE [auth].[users] SET password = 'J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=' WHERE username = '<username>'
   ```

## <a name="change-azdata_password-in-the-sql-server-master-instance"></a>變更 SQL Server 主要執行個體中的 `AZDATA_PASSWORD`

1. 使用任何系統管理員使用者連線到主要 SQL 端點。

1. 若要變更部署期間您在參數 `AZDATA_USERNAME` 中定義的登入認證密碼，請執行下列 TSQL 命令：

   ```sql
   ALTER LOGIN <AZDATA_USERNAME> WITH PASSWORD = 'newPassword'
   ```
