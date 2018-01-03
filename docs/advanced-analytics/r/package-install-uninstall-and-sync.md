---
title: "SQL Server 的 R 封裝同步 |Microsoft 文件"
ms.custom: 
ms.date: 10/02/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7530d67c2c74b4918228ea91597f1667c0abbd6
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server 的 R 封裝同步處理

SQL Server 2017 包含了可同步處理的檔案系統和執行個體與資料庫之間使用封裝的 R 封裝的集合。
這項功能提供給更輕鬆地備份 SQL Server 資料庫與相關聯的 R 封裝集合。 使用這項功能，系統管理員可以還原不只是在資料庫中，但是任何使用該資料庫中的資料科學家所使用的 R 封裝。

本主題描述封裝的同步處理功能，以及如何使用[rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)函式來執行下列工作：

+ 同步處理整個 SQL Server 資料庫的封裝清單

+ 同步處理個別使用者或使用者群組所使用的封裝

+ 如果使用者移到不同的 SQL Server，您可以使用使用者的工作資料庫的備份，並將它還原到新的伺服器，和使用者的套件會安裝到所需的 r 新的伺服器上的檔案系統

例如，您可能會在這些案例中使用封裝同步處理：

+ DBA 已還原至新的機器的 SQL Server 執行個體，並要求使用者從其 R 用戶端連接及執行`rxSyncPackages`重新整理，然後還原其封裝。

+ 您將 R 封裝，在檔案系統上的已損毀，因此您執行`rxSyncPackages`SQL Server 上。

## <a name="requirements"></a>需求

您可以使用封裝的同步處理之前，您必須擁有適當版本的 Microsoft R，並啟用相關的資料庫功能。

### <a name="determine-whether-your-server-supports-package-management"></a>判斷您的伺服器是否支援封裝管理

這個功能就可以在 SQL Server 2017 CTP 2 或更新版本。

由於這項功能會使用 Microsoft R 版本 9.1.0 中 R 函式，您可以加入這項功能的 SQL Server 2016 執行個體的執行個體升級為使用最新版的 Microsoft。如需詳細資訊，請參閱[升級 SQL Server R services 使用 SqlBindR.exe](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="enable-the-package-management-feature"></a>啟用封裝管理功能

若要使用封裝的同步處理需要個別用於執行 R 工作的資料庫和 SQL Server 執行個體上啟用新的封裝管理功能。

1. 伺服器系統管理員可讓 SQL Server 執行個體的功能。
2. 每個資料庫，系統管理員會授與使用者的能力，安裝或共用的 R 封裝。

完成此動作後，使用者和他們已安裝的套件相關資訊會儲存在 SQL Server 執行個體。 您可以接著套用這項資訊來更新檔案系統中的 R 封裝。

每當您將新的封裝，封裝管理函式的使用，會更新 SQL Server 和檔案系統中的兩筆記錄。

> [!NOTE]
> 如果您有已安裝的 R 封裝的傳統方法，直接在檔案系統中安裝的封裝中使用的 R 工具，您無法使用封裝的同步處理。
### <a name="permissions"></a>Permissions

+ 執行封裝的同步處理函式的人員必須是安全性主體在 SQL Server 執行個體和具有之封裝的資料庫。

+ 函式的呼叫端必須是其中一個這些封裝管理角色的成員： **rpkgs 共用**或**rpkgs 私用**。

+ 若要同步處理封裝標示為**共用**，正在執行的函式的人員必須擁有成員資格**rpkgs 共用**角色，然後在移動封裝必須已安裝到共用範圍程式庫。

+ 若要同步處理封裝標示為**私人**，可能是系統管理員或封裝的擁有者必須執行函式，並封裝必須是私用。

+ 若要同步處理封裝代表其他使用者，擁有者必須是隸屬**db_owner**資料庫角色。

## <a name="how-package-synchronization-works"></a>封裝同步化的運作方式

若要使用封裝的同步處理，呼叫[rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)，這是新的函式中[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)。 您可以呼叫此函式使用 sp_execute_external_script，從 SQL Server，或您可以從遠端的 R 用戶端執行，並指定 SQL Server 計算內容。 

因為封裝的管理是在資料庫層級，每次呼叫`rxSyncPackages`，您必須指定 SQL Server 執行個體和資料庫，然後列出封裝，或是指定封裝範圍。

1. 建立 SQL Server 計算內容使用`RxInSqlServer`函式。 如果您未指定的計算內容，則會使用目前的計算內容。

2. 指定的計算內容中執行個體上提供資料庫的名稱。 封裝管理每個資料庫。

3. 列出要同步處理的封裝。

4.  （選擇性） 使用*範圍*引數以指示是否正在同步處理為單一使用者，或使用者群組的套件。 如果您在執行函式未指定**私人**或**共用**的範圍，請整組可用的所有領域的封裝，並將複製的使用者。

如果命令執行成功，檔案系統中現有的封裝會加入至資料庫，使用指定的範圍和擁有者。 如果檔案系統損毀時，會還原封裝，根據資料庫中維護的清單。

### <a name="example-1-synchronize-all-package-by-database"></a>範例 1： 資料庫同步處理所有的封裝

這個範例會取得所有封裝安裝在資料庫中 [TestDB]。 因為沒有擁有者是特定項目，此清單包含已安裝的私用和共用範圍的所有封裝。

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>範例 2： 限制已同步處理對封裝進行範圍

下列範例會同步處理指定之範圍中的封裝。

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>範例 3。 限制已同步處理的封裝擁有者

下列範例示範如何取得特定使用者的已安裝的封裝。 在此範例中，SQL 登入名稱來識別使用者*user1*。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

### <a name="example-4-restrict-synchronized-packages-by-owner"></a>範例 4。 限制已同步處理的封裝擁有者

下列範例會同步處理管理資料庫中的封裝清單之檔案系統中已安裝的套件。 如果遺漏任何封裝，它會安裝在檔案系統。

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="related-resources"></a>相關資源

[SQL Server 的 R 套件管理](r-package-management-for-sql-server-r-services.md)
