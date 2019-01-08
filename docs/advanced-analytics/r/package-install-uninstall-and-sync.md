---
title: 從檔案系統-SQL Server Machine Learning 服務的 R 套件同步處理
description: 更新檔案系統上安裝較新版本的 SQL Server 上的 R 程式庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5b7141e1fe6256c7a7e21056d82f2d8fc4ad4faf
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431815"
---
# <a name="r-package-synchronization-for-sql-server"></a>適用於 SQL Server 的 R 套件同步處理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR SQL Server 2017 中隨附的版本包括能夠同步處理的檔案系統和執行個體與資料庫之間使用封裝的 R 套件的集合。

這項功能可讓您更輕鬆地備份 SQL Server 資料庫相關聯的 R 封裝集合。 使用這項功能，以系統管理員可以還原不只是資料庫，但是任何使用該資料庫中的資料科學家所使用的 R 套件。

這篇文章描述封裝的同步處理功能，以及如何使用[rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)函式來執行下列工作：

+ 同步處理整個 SQL Server 資料庫的封裝清單

+ 同步處理個別的使用者，或一群使用者使用的套件

+ 如果使用者移至不同的 SQL Server，您可以在使用者的工作資料庫的備份，並將它還原到新的伺服器，以及使用者的套件會安裝到所需的 r 新的伺服器上的檔案系統

比方說，您可能會在這些情況下，使用套件同步處理：

+ DBA 已還原至新的機器的 SQL Server 的執行個體，並要求使用者從其 R 用戶端連線，並執行`rxSyncPackages`重新整理，然後還原其套件。

+ 您將檔案系統上的 R 封裝已損毀，讓您執行`rxSyncPackages`SQL Server 上。

## <a name="requirements"></a>需求

您可以使用套件同步處理之前，您必須擁有適當版本的 Microsoft R 或 Machine Learning Server。 這項功能可在 Microsoft R 版本 9.1.0 或更新版本。 

您也必須啟用[封裝管理功能](r-package-how-to-enable-or-disable.md)伺服器上。

### <a name="determine-whether-your-server-supports-package-management"></a>判斷您的伺服器是否支援套件管理

這項功能是適用於 SQL Server 2017 CTP 2 或更新版本。

您也可以升級的執行個體，以使用最新版的 Microsoft R 的 SQL Server 2016 執行個體新增此功能如需詳細資訊，請參閱 <<c0> [ 使用 SqlBindR.exe 升級 SQL Server R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="enable-the-package-management-feature"></a>啟用封裝管理功能

若要使用套件同步處理需要個別的資料庫和 SQL Server 執行個體上，啟用新的封裝管理功能。 如需詳細資訊，請參閱 <<c0> [ 啟用或停用封裝管理適用於 SQL Server](r-package-how-to-enable-or-disable.md)。

1. 伺服器系統管理員可讓 SQL Server 執行個體的功能。
2. 針對每個資料庫中，系統管理員授與個別使用者的能力安裝或共用 R 封裝，使用 資料庫角色。

完成時，您可以使用 RevoScaleR 函式，例如[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)將套件安裝到資料庫。  使用者與他們可以使用封裝的相關資訊會儲存在 SQL Server 執行個體。 

每當您將新的封裝，使用封裝管理函數時，會更新這兩個 SQL Server 和檔案系統中的記錄。 這項資訊可用來還原整個資料庫的封裝資訊。

### <a name="permissions"></a>Permissions

+ 執行封裝的同步處理函式的人員必須是安全性主體上的 SQL Server 執行個體和資料庫具有封裝。

+ 函式的呼叫者必須是其中一個封裝管理角色的成員： **rpkgs 共用**或是**rpkgs 私用**。

+ 同步處理封裝標示**共用**，執行函式的人員必須擁有成員資格**rpkgs 共用**角色，以及要移動的封裝必須已安裝到共用範圍程式庫。

+ 同步處理封裝標示**私人**，以系統管理員或封裝的擁有者必須執行函式，或封裝必須是私用。

+ 若要同步處理使用者代表其他使用者的套件，擁有者必須 bhe 隸屬**db_owner**資料庫角色。

## <a name="how-package-synchronization-works"></a>封裝的同步處理運作方式

若要使用套件同步處理，呼叫[rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)，這是新的函式，在[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。 

每次呼叫`rxSyncPackages`，您必須指定 SQL Server 執行個體和資料庫。 然後，列出的套件進行同步處理，或指定封裝的範圍。

1. 建立 SQL Server 計算內容使用`RxInSqlServer`函式。 如果您未指定計算內容，則會使用目前的計算內容。

2. 指定的計算內容中執行個體上提供資料庫的名稱。 封裝會同步處理每個資料庫。

3. 指定要使用的範圍引數同步處理的封裝。

    如果您使用**私人**同步處理範圍內，指定擁有者所擁有的唯一封裝。 如果您指定**共用**同步處理範圍，在資料庫中的所有非私用封裝。 
    
    如果您沒有指定執行函式**私人**或**共用**範圍內，所有的封裝會同步處理。

4. 如果命令成功時，就會將檔案系統中現有的封裝新增至資料庫，使用指定的範圍和擁有者。

    如果檔案系統損毀，依據資料庫中維護的清單還原套件。

    如果封裝管理功能不適用於目標資料庫，則會引發錯誤：「 封裝管理功能可能是未啟用 SQL Server 上或版本不太舊 」

### <a name="example-1-synchronize-all-package-by-database"></a>範例 1： 所有的套件同步處理資料庫

此範例會從本機檔案系統中取得任何新套件，並將套件安裝資料庫 [TestDB] 中。 因為沒有擁有者是特定項目，此清單會包含已安裝的私用和共用範圍的所有封裝。

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>範例 2： 限制範圍內的同步處理的封裝

下列範例會同步處理指定之範圍中的封裝。

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>範例 3。 限制已同步處理的套件擁有者

下列範例示範如何同步處理特定的使用者安裝的套件。 SQL 登入名稱，在此範例中，識別使用者*user1*。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>相關資源

[SQL Server 的 R 套件管理](install-additional-r-packages-on-sql-server.md)
