---
title: 從檔案系統進行 R 套件同步
description: 使用安裝在檔案系統上的較新版本來更新 SQL Server 上的 R 程式庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 71ff0b6232eb69af7e5e138d2681f8126a12d915
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74485253"
---
# <a name="r-package-synchronization-for-sql-server"></a>適用於 SQL Server 的 R 套件同步
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

包含在 SQL Server 2017 中的 RevoScaleR 版本具有在檔案系統，以及使用套件所在的執行個體和資料庫之間同步 R 套件集合的能力。

提供此功能的目的，是為了讓使用者能較輕鬆地備份與 SQL Server 資料庫相關聯的 R 套件集合。 透過使用此功能，系統管理員不僅可以還原資料庫，更可以還原使用該資料庫的資料科學家所使用的任何 R 套件。

此文章描述套件同步功能，以及如何使用 [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) \(英文\) 函式來執行下列工作：

+ 同步整個 SQL Server 資料庫的套件清單

+ 同步個別使用者或使用者群組所使用的套件

+ 如果使用者移到不同的 SQL Server，您可以備份該使用者正在使用的資料庫，並將其還原到新的伺服器，而該使用者的套件將會依照 R 的需求，安裝到新伺服器上的檔案系統。

例如，您可能會在這些案例中使用套件同步：

+ DBA 已將 SQL Server 的執行個體還原至新的電腦，並要求使用者從其 R 用戶端連線，並執行 `rxSyncPackages` 以重新整理及還原其套件。

+ 您認為檔案系統上的某個 R 套件已損毀，因此您在 SQL Server 上執行 `rxSyncPackages`。

## <a name="requirements"></a>需求

在您可以使用套件同步之前，您必須具有適當版本的 Microsoft R 或 Machine Learning Server。 此功能已在 Microsoft R 9.1.0 版或更新版本中提供。 

您也必須在伺服器上啟用[套件管理功能](r-package-how-to-enable-or-disable.md)。

### <a name="determine-whether-your-server-supports-package-management"></a>判斷伺服器是否支援套件管理

此功能在 SQL Server 2017 CTP 2 或更新版本中提供。

您可以將此功能新增到 SQL Server 2016 的執行個體，方法是將該執行個體升級至最新版本的 Microsoft R。如需詳細資訊，請參閱[使用 SqlBindR.exe 來升級 SQL Server R Services](../install/upgrade-r-and-python.md)。

### <a name="enable-the-package-management-feature"></a>啟用套件管理功能

若要使用套件同步，必須在 SQL Server 執行個體及個別的資料庫上啟用新的套件管理功能。 如需詳細資訊，請參閱[啟用或停用 SQL Server 的套件管理](r-package-how-to-enable-or-disable.md)。

1. 伺服器管理員會為 SQL Server 執行個體啟用該功能。
2. 針對每個資料庫，系統管理員會使用資料庫角色，將安裝或共用 R 套件的能力授與個別使用者。

完成此作業之後，您便可以使用 RevoScaleR 函式 (例如 [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) \(英文\)) 來將套件安裝到資料庫。  關於使用者及其所能使用之套件的相關資訊會儲存在 SQL Server 執行個體中。 

每當您使用套件管理函式來新增套件時，系統將會同時更新 SQL Server 和檔案系統中的記錄。 此資訊可以用來還原整個資料庫的套件資訊。

### <a name="permissions"></a>權限

+ 執行套件同步函式的人員必須是具有套件的 SQL Server 執行個體和資料庫上的安全性主體。

+ 函式的呼叫者必須是這些套件管理角色之一的成員：**rpkgs-shared** 或 **rpkgs-private**。

+ 若要同步標記為 **shared** 的套件，執行函式的人員必須具有 **rpkgs-shared** 角色的成員資格，且要移動的套件必須已安裝到共用範圍的程式庫。

+ 若要同步標記為 **private** 的套件，函式必須由套件擁有者或系統管理員執行，且套件必須為私人。

+ 若要代表其他使用者同步套件，擁有者必須是 **db_owner** 資料庫角色的成員。

## <a name="how-package-synchronization-works"></a>套件同步如何運作

若要使用套件同步，請呼叫 [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages) \(英文\)，其為 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\) 中的新函式。 

針對每個對 `rxSyncPackages` 的呼叫，您必須指定 SQL Server 執行個體和資料庫。 然後，請列出要同步的套件，或是指定套件範圍。

1. 使用 `RxInSqlServer` 函式來建立 SQL Server 計算內容。 如果您不指定計算內容，系統會使用目前的計算內容。

2. 提供指定計算內容中執行個體上的資料庫名稱。 套件會針對每個資料庫進行同步。

3. 使用範圍引數來指定要同步的套件。

    如果您使用 **private** 範圍，只有由特定擁有者所擁有的套件才會同步。 如果您指定 **shared** 範圍，則會同步資料庫中的所有非私人套件。 
    
    若您在沒有指定 **private** 或 **shared** 範圍的情況下執行函式，系統會同步所有套件。

4. 如果命令成功，檔案系統中的現有套件將會搭配指定的範圍和擁有者新增到資料庫。

    如果檔案系統已損毀，套件會根據資料庫中維護的清單進行還原。

    如果目標資料庫上沒有套件管理功能可用，就會引發錯誤：「套件管理功能未在 SQL Server 上啟用或版本太舊」

### <a name="example-1-synchronize-all-package-by-database"></a>範例 1. 依資料庫同步所有套件

此範例會從本機檔案系統取得所有新套件，然後將套件安裝到資料庫 [TestDB] 中。 由於沒有指定擁有者，因此清單會包含針對私人和共用範圍安裝的所有套件。

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>範例 2. 依範圍限制同步套件

下列範例只會同步指定範圍中的套件。

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>範例 3. 依擁有者限制同步套件

下列範例示範如何僅同步針對特定使用者安裝的套件。 在此範例中，使用者是透過 SQL 登入名稱 *user1* 來識別。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>相關資源

[SQL Server 的 R 套件管理](install-additional-r-packages-on-sql-server.md)