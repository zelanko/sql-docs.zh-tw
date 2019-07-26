---
title: 從檔案系統進行 R 封裝同步處理
description: 使用安裝在檔案系統上的較新版本, 更新 SQL Server 上的 R 程式庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: d4af7822dbabeb64816182c245617ffebc3b61c7
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470181"
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server 的 R 封裝同步處理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2017 中包含的 RevoScaleR 版本包括能夠在檔案系統與使用封裝的實例和資料庫之間同步處理 R 封裝的集合。

這項功能的目的是為了讓您更輕鬆地備份與 SQL Server 資料庫相關聯的 R 套件集合。 系統管理員可以使用這項功能來還原資料庫, 而不只是資料科學家在該資料庫中工作所使用的任何 R 封裝。

本文說明封裝同步處理功能, 以及如何使用[rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)函式來執行下列工作:

+ 同步處理整個 SQL Server 資料庫的封裝清單

+ 同步處理個別使用者或使用者群組所使用的套件

+ 如果使用者移至不同的 SQL Server, 您可以備份使用者的工作資料庫, 並將它還原到新的伺服器, 然後將使用者的套件安裝到新伺服器上的檔案系統, 如 R 所需。

例如, 您可以在這些案例中使用封裝同步處理:

+ DBA 已將 SQL Server 的實例還原到新機器, 並要求使用者從其 R 用戶端進行連線, 並`rxSyncPackages`執行以重新整理和還原其套件。

+ 您認為檔案系統上的 R 封裝已損毀, 因此您`rxSyncPackages`可以在 SQL Server 上執行。

## <a name="requirements"></a>需求

在您可以使用封裝同步處理之前, 您必須擁有適當版本的 Microsoft R 或 Machine Learning Server。 這項功能是在 Microsoft R 版本9.1.0 或更新版本中提供。 

您也必須在伺服器上啟用[封裝管理功能](r-package-how-to-enable-or-disable.md)。

### <a name="determine-whether-your-server-supports-package-management"></a>判斷您的伺服器是否支援套件管理

這項功能適用于 SQL Server 2017 CTP 2 或更新版本。

您可以藉由將實例升級為使用最新版的 Microsoft R, 將此功能新增至 SQL Server 2016 的實例。如需詳細資訊, 請參閱[使用 SqlBindR 升級 SQL Server R Services](../install/upgrade-r-and-python.md)。

### <a name="enable-the-package-management-feature"></a>啟用套件管理功能

若要使用封裝同步處理, 您需要在 SQL Server 實例和個別資料庫上啟用新的封裝管理功能。 如需詳細資訊, 請參閱[啟用或停用 SQL Server 的封裝管理](r-package-how-to-enable-or-disable.md)。

1. 伺服器管理員會啟用 SQL Server 實例的功能。
2. 系統管理員會針對每個資料庫, 使用資料庫角色, 授與個別使用者安裝或共用 R 套件的能力。

完成此動作時, 您可以使用 RevoScaleR 函式, 例如[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)將封裝安裝到資料庫中。  使用者及其可使用之封裝的相關資訊會儲存在 SQL Server 實例中。 

每當您使用封裝管理功能來新增封裝時, SQL Server 和檔案系統中的記錄都會更新。 這份資訊可以用來還原整個資料庫的封裝資訊。

### <a name="permissions"></a>Permissions

+ 執行封裝同步處理函式的人員, 必須是包含封裝之 SQL Server 實例和資料庫的安全性主體。

+ 函式的呼叫者必須是下列其中一個封裝管理角色的成員: **rpkgs-private-shared**或**rpkgs-private-private**。

+ 若要同步處理標記為**共用**的封裝, 執行該函式的人員必須擁有**rpkgs-private 共用**角色的成員資格, 而且要移動的套件必須已安裝到共用範圍程式庫。

+ 若要同步處理標示為**私**用的封裝, 封裝的擁有者或系統管理員必須執行此函式, 而且這些封裝必須是私用的。

+ 若要代表其他使用者同步處理封裝, 擁有者必須是**db_owner**資料庫角色的成員。

## <a name="how-package-synchronization-works"></a>封裝同步處理的運作方式

若要使用封裝同步處理, 請呼叫[rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), 這是[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)中的新函式。 

對於的每個`rxSyncPackages`呼叫, 您都必須指定 SQL Server 實例和資料庫。 然後, 列出要同步處理的封裝, 或指定封裝範圍。

1. 使用`RxInSqlServer`函數來建立 SQL Server 計算內容。 如果您未指定計算內容, 則會使用目前的計算內容。

2. 在指定的計算內容中, 提供實例上的資料庫名稱。 封裝會針對每個資料庫進行同步處理。

3. 使用 scope 引數指定要同步處理的封裝。

    如果您使用**私**用範圍, 則只會同步處理指定的擁有者所擁有的封裝。 如果您指定**共用**範圍, 則資料庫中的所有非私用封裝都會進行同步處理。 
    
    如果您在未指定**私**用或**共用**範圍的情況下執行函數, 則會同步處理所有封裝。

4. 如果命令成功, 檔案系統中的現有封裝會新增至資料庫, 並具有指定的範圍和擁有者。

    如果檔案系統已損毀, 則會根據資料庫中維護的清單來還原封裝。

    如果目標資料庫上的封裝管理功能無法使用, 就會引發錯誤:「套件管理功能未在 SQL Server 上啟用, 或版本太舊」

### <a name="example-1-synchronize-all-package-by-database"></a>範例 1： 依資料庫同步處理所有封裝

這個範例會從本機檔案系統取得任何新的封裝, 並將封裝安裝在資料庫 [TestDB] 中。 因為沒有特定擁有者, 此清單會包含已針對私人和共用範圍安裝的所有封裝。

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>範例 2： 依範圍限制同步的封裝

下列範例只會同步處理指定範圍內的封裝。

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>範例3。 依擁有者限制同步處理的封裝

下列範例示範如何只同步處理針對特定使用者安裝的封裝。 在此範例中, 使用者是以 SQL 登入名稱*user1*來識別。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>相關資源

[SQL Server 的 R 套件管理](install-additional-r-packages-on-sql-server.md)
