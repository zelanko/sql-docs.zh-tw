---
title: SQL Server 的 R 封裝同步 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6e0fe3fa36a5a330e1b4fee926c0d2e4b10d809f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server 的 R 封裝同步處理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

包含在 SQL Server 2017 RevoScaleR 的版本包含了可同步處理的檔案系統和執行個體與資料庫之間使用封裝的 R 封裝的集合。

這項功能提供給更輕鬆地備份 SQL Server 資料庫與相關聯的 R 封裝集合。 使用這項功能，系統管理員可以還原不只是在資料庫中，但是任何使用該資料庫中的資料科學家所使用的 R 封裝。

這篇文章描述封裝的同步處理功能，以及如何使用[rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)函式來執行下列工作：

+ 同步處理整個 SQL Server 資料庫的封裝清單

+ 同步處理個別使用者或使用者群組所使用的封裝

+ 如果使用者移到不同的 SQL Server，您可以使用使用者的工作資料庫的備份，並將它還原到新的伺服器，和使用者的套件會安裝到所需的 r 新的伺服器上的檔案系統

例如，您可能會在這些案例中使用封裝同步處理：

+ DBA 已還原至新的機器的 SQL Server 執行個體，並要求使用者從其 R 用戶端連接及執行`rxSyncPackages`重新整理，然後還原其封裝。

+ 您將 R 封裝，在檔案系統上的已損毀，因此您執行`rxSyncPackages`SQL Server 上。

## <a name="requirements"></a>需求

您可以使用封裝的同步處理之前，您必須適當版本的 Microsoft R Server 機器學習。 這項功能被提供 Microsoft R 版本 9.1.0 或更新版本。 

您也必須啟用[封裝管理功能](r-package-how-to-enable-or-disable.md)在伺服器上。

### <a name="determine-whether-your-server-supports-package-management"></a>判斷您的伺服器是否支援封裝管理

這個功能就可以在 SQL Server 2017 CTP 2 或更新版本。

您可以加入這項功能的 SQL Server 2016 執行個體的執行個體升級為使用最新版的 Microsoft。如需詳細資訊，請參閱[升級 SQL Server R Services 使用 SqlBindR.exe](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="enable-the-package-management-feature"></a>啟用封裝管理功能

若要使用封裝的同步處理需要個別的資料庫和 SQL Server 執行個體上啟用新的封裝管理功能。 如需詳細資訊，請參閱[啟用或停用的 SQL Server 的封裝管理](r-package-how-to-enable-or-disable.md)。

1. 伺服器系統管理員可讓 SQL Server 執行個體的功能。
2. 每個資料庫，系統管理員授與個別使用者的能力安裝或共用的 R 封裝，使用資料庫角色。

完成此動作後，您可以使用 RevoScaleR 函式，例如[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)封裝安裝到資料庫。  使用者和他們可以使用封裝資訊儲存在 SQL Server 執行個體。 

每當您將新的封裝，封裝管理函式的使用，會更新 SQL Server 和檔案系統中的兩筆記錄。 這項資訊可以用來還原整個資料庫的封裝資訊。

### <a name="permissions"></a>Permissions

+ 執行封裝的同步處理函式的人員必須是安全性主體在 SQL Server 執行個體和具有之封裝的資料庫。

+ 函式的呼叫端必須是其中一個這些封裝管理角色的成員： **rpkgs 共用**或**rpkgs 私用**。

+ 若要同步處理封裝標示為**共用**，正在執行的函式的人員必須擁有成員資格**rpkgs 共用**角色，然後在移動封裝必須已安裝到共用範圍程式庫。

+ 若要同步處理封裝標示為**私人**，可能是系統管理員或封裝的擁有者必須執行函式，並封裝必須是私用。

+ 若要同步處理封裝代表其他使用者，擁有者必須 bhe 隸屬**db_owner**資料庫角色。

## <a name="how-package-synchronization-works"></a>封裝同步化的運作方式

若要使用封裝的同步處理，呼叫[rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)，這是新的函式中[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。 

每次呼叫`rxSyncPackages`，您必須指定 SQL Server 執行個體和資料庫。 然後，列出要同步處理時，封裝，或指定封裝的範圍。

1. 建立 SQL Server 計算內容使用`RxInSqlServer`函式。 如果您未指定的計算內容，則會使用目前的計算內容。

2. 指定的計算內容中執行個體上提供資料庫的名稱。 封裝會同步處理每個資料庫。

3. 指定要使用的範圍引數來同步處理的封裝。

    如果您使用**私人**同步處理範圍，僅限指定的擁有者所擁有的套件。 如果您指定**共用**同步處理範圍，在資料庫中的所有非私用封裝。 
    
    如果您在執行函式未指定**私人**或**共用**範圍內，所有的封裝會同步處理。

4. 如果命令成功時，檔案系統中現有的封裝會加入至資料庫，使用指定的範圍和擁有者。

    如果檔案系統損毀時，會還原封裝，根據資料庫中維護的清單。

    如果封裝管理功能無法使用目標資料庫上，會引發錯誤:"的封裝管理功能未啟用，或者在 SQL Server 上，或版本太舊 」

### <a name="example-1-synchronize-all-package-by-database"></a>範例 1： 資料庫同步處理所有的封裝

這個範例會從本機檔案系統中取得新的封裝，並會在資料庫 [TestDB] 中安裝的套件。 因為沒有擁有者是特定項目，此清單包含已安裝的私用和共用範圍的所有封裝。

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

下列範例會示範如何同步處理的特定使用者的已安裝的封裝。 在此範例中，SQL 登入名稱來識別使用者*user1*。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>相關資源

[SQL Server 的 R 套件管理](r-package-management-for-sql-server-r-services.md)
