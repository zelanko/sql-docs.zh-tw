---
title: "封裝安裝、 解除安裝，以及同步 |Microsoft 文件"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 959282395d178a090a3d447769ced4dca8882f89
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---

# <a name="r-package-synchronization-for-sql-server"></a>SQL Server 的 R 封裝同步處理

SQL Server 2017 CTP 2.0 包含新的函式之同步處理的 R 封裝，以支援備份和還原的 SQL Server 資料庫與相關聯的 R 封裝集合。 這項功能可協助確保使用者所建立的 R 封裝的複雜設定不會遺失，而且可以輕鬆地還原。  

本主題描述封裝的同步處理功能的作用，以及如何使用`rxSyncPackages()`函式來執行下列工作：

+  同步處理整個 SQL Server 資料庫的封裝清單
+  使用個別使用者或使用者群組的同步處理封裝

> [!NOTE]
> 此函式提供發行前版本軟體的一部分，並可能有所變更，最終發行前。

## <a name="what-is-package-synchronization"></a>何謂封裝同步處理 

封裝的同步處理的新功能，特別適用於 SQL Server 計算內容。 它被設計來取得特定的資料庫中，為特定使用者或群組所安裝的 R 封裝的清單，並確認封裝列在檔案系統的相符項目與資料庫中。 

這是需要移動使用者資料庫和移動資料庫以及封裝時相當實用。 當您備份和還原 SQL Server 資料庫，用於 R 工作時，您也可以使用封裝的同步處理。

封裝的同步處理所使用的新函式， `rxSyncPackages()`。 若要同步的封裝清單，您可以開啟 R 命令提示字元、 傳遞的執行個體和您想要使用的資料庫定義的計算內容，然後提供封裝範圍或使用者或擁有者名稱。 

### <a name="how-packages-are-managed-in-r-and-sql-server"></a>如何在 R 和 SQL Server 管理套件

一般而言，當您執行 R 指令碼使用標準的 R 工具，R 封裝會安裝在檔案系統上。 如果有多人在同一部電腦上使用 R，可能會有許多相同的封裝，在不同的資料夾，或不同的使用者文件庫中的複本。

不過，若要使用從 SQL Server R 封裝，封裝必須安裝在執行個體相關聯的預設 R 程式庫。 多個啟用，R 與 SQL Server 執行個體可能裝載伺服器電腦，並在此情況下，每個執行個體可以有一組個別的 R 封裝。 

資料庫管理員負責安裝封裝的執行個體上。 不過，封裝管理程式庫，系統管理員可以委派此責任給使用者。 

+ 每個資料庫，系統管理員就能給予使用者能夠自由地安裝所需的 R 封裝。 這項機制可確保多個使用者可以安裝不同版本的 R 封裝，而不會造成衝突的 SQL Server 電腦的其他使用者。 個別使用者可以安裝自己使用，套件使用標示為的檔案系統位置**私人**，如果其所屬的資料庫角色**rpkgs 私用**。

+ 系統管理員可以設定在資料庫上，封裝使用者的群組，並安裝共用的所有使用者群組中的封裝。 封裝可以共用資料庫角色的成員**rpkgs 共用**。 這類使用者也可以將封裝安裝到私用範圍的位置。 

### <a name="goal-of-package-synchronization"></a>封裝的同步處理的目標

如果伺服器上的資料庫遺失，或必須移動，利用封裝同步處理，您可以還原特定的封裝集至資料庫、 使用者或群組。 

使用者和安裝軟體套件的相關資訊會儲存在 SQL Server 執行個體，並用來更新檔案系統中的封裝。 每當您將新的封裝，封裝管理函式的使用，會更新 SQL Server 和檔案系統中的兩筆記錄。 因此，如果使用者移到不同的 SQL Server，您可以使用使用者的工作資料庫的備份，並將它還原到新的伺服器，而且使用者的套件會安裝到所需的 r 新的伺服器上的檔案系統


### <a name="supported-versions"></a>支援的版本

此函式包含在 SQL Server 2017 CTP 2.0 中。

因為此函式是 Microsoft R 版本 9.1.0 的一部分，您可以將這項功能加入 SQL Server 2016 的執行個體的執行個體升級為使用最新版的 Microsoft。如需詳細資訊，請參閱[升級 SQL Server R services 使用 SqlBindR.exe](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="to-synchronize-packages"></a>若要同步處理封裝

您呼叫`rxSyncPackages`之後，請將 SQL Server 執行個體還原到新的電腦，或如果 R 封裝在檔案系統上確認已損毀。

如果命令執行成功，檔案系統中現有的封裝會新增至資料庫、 範圍及所指定的擁有者。 如果檔案系統損毀時，封裝就會是 restred 根據資料庫中維護的清單。

### <a name="syntax"></a>語法
`rxSyncPackages(computeContext = rxGetOption("computeContext"),  scope = c("shared", "private"), owner = c(), verbose = getOption("verbose"))`

+ 計算內容

    定義組成的執行個體和資料庫，然後同步處理封裝的 SQL Server 計算內容。使用建立 SQ Server 內容`RxInSqlServer`函式。 如果您未指定的計算內容，則會使用目前的計算內容。 

+ 範圍。

  指出您要安裝為單一使用者，或使用者群組的套件： 

    + **私用**作業將會包含只有在有已指定的擁有者所安裝的封裝。
    + **共用**oepration 會包含所有的使用者群組所安裝的封裝。 

  如果您未指定私用或共用的範圍中執行函式，會套用兩個領域。 如此一來，將複製的整組所有範圍和使用者可用的封裝。

+ 擁有者 

    指定要同步處理之封裝的擁有者。 擁有者名稱必須是有效的 SQL 資料庫使用者。 如果您將保留空白，則會使用在連接中指定的 SQL 登入的使用者名稱。


### <a name="requirements"></a>需求

+ 執行的函式的人員必須是安全性主體上的 SQL Server 執行個體和資料庫有封裝，而且必須是封裝管理角色的成員： **rpkgs 共用**或**rpkgs 私用** 
  + 若要同步處理封裝標示為**共用**，正在執行的函式的人員必須擁有成員資格**rpkgs 共用**角色，然後在移動封裝必須已安裝到共用範圍程式庫。
  + 標示為還套件**私人**，可能是系統管理員或封裝的擁有者必須執行函式，並封裝必須是私用。
+ **rpkgs 使用者**-這個角色的成員可以執行程式碼會使用 SQL Server 執行個體上安裝的封裝，但是您無法安裝或同步處理封裝。
+ 若要同步代表其他使用者的封裝，擁有者必須是成員**db_owner**資料庫角色。

## <a name="examples"></a>範例

下列範例會建立特定 SQL Server 執行個體的連接、 指定資料庫，，然後指定一組封裝，來同步處理。 

當呼叫`rxSyncPackages`進行時，清單會在檔案系統與資料庫之間同步處理的封裝。 

### <a name="synchronize-all-by-database"></a>所有同步處理資料庫

這個範例會取得所有封裝安裝在資料庫中 [TestDB]。 因為沒有擁有者是特定項目，此清單包含已安裝的私用和共用範圍的所有封裝。

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-scope"></a>限制已同步處理對封裝進行範圍 

下列範例同步處理共用的範圍或私用範圍中的封裝。

**共用範圍**

```R
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)
```

**私用範圍**

```R
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-owner"></a>限制已同步處理的封裝擁有者 

下列範例示範如何取得特定使用者的已安裝的封裝。 在此範例中，SQL 登入名稱來識別使用者*user1*。

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="see-also"></a>另請參閱

[SQL Server 的 R 封裝管理](../r/r-package-management-for-sql-server-r-services.md)
