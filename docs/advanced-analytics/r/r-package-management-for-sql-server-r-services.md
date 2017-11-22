---
title: "SQL Server 的 R 封裝管理 |Microsoft 文件"
ms.custom: 
ms.date: 10/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d53965dd5e931eb4290031ed2023cdb78ee74283
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="r-package-management-for-sql-server"></a>SQL Server 的 R 封裝管理

本文描述 SQL Server 2017 和 SQL Server 2016 中的 R 封裝的管理功能。

+ 2017 2016年之間的 R 封裝安裝方法中的變更
+ 管理 R 封裝的建議的方法
+ 新的資料庫角色的 SQL Server 2017 封裝管理
+ 新的 T-SQL 陳述式的 SQL Server 2017 封裝管理

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

## <a name="differences-in-package-management-between-sql-server-2016-and-sql-server-2017"></a>封裝管理 SQL Server 2016 和 SQL Server 2017 之間的差異

在**SQL Server 2017**，您可以啟用封裝管理執行個體層級，並管理使用者權限，以新增或使用資料庫層級的封裝。

這需要資料庫管理員，啟用執行指令碼會建立必要資料庫物件的封裝管理功能。 如需詳細資訊，請參閱[如何啟用 R 封裝管理](r-package-how-to-enable-or-disable.md)。

在**SQL Server 2016**，系統管理員必須安裝在執行個體相關聯的 R 程式庫中的 R 封裝。 所有使用者執行個體中執行 R 程式碼會都使用這些封裝。 SQL server 中執行的 R 程式碼無法使用安裝在使用者程式庫中的封裝。 不過，系統管理員可以授與個別使用者執行特定資料庫內的 R 指令碼的能力。

**差異及優點的摘要**

+ 如果您在 SQL Server 2017 使用機器學習服務，您可以管理和安裝的 R 封裝使用的傳統方法，根據 R 工具，或藉由使用新的資料庫角色和 T-SQL 陳述式。

+ 我們建議您在第二個方法，因為它提供更細微的控制，由系統管理員，結合其他更多的自由，讓使用者。 例如，使用者可以安裝自己的封裝，請使用預存程序或 R 程式碼以及與其他人共用封裝。 

    因為封裝可以限定在資料庫中，而且每個使用者取得隔離的套件沙箱，所以很容易安裝不同版本的相同的 R 封裝。 也很容易，您可以複製或移動資料庫之間的使用者和其封裝。 

+ 使用 SQL Server 中的封裝管理功能可讓您更容易備份和還原作業。 當您將工作資料庫移轉至新的伺服器時，您可以使用封裝的同步處理函式來讀取您的封裝清單，並將其安裝在新的伺服器上的資料庫。

+ 您可能會發現的電腦上，如果您是唯一的人使用機器學習工作的伺服器，使用傳統的 R 工具，以系統管理員身分安裝 R 封裝更方便。

+ 如果您使用 SQL Server 2016 R 服務，您應該繼續安裝 R 封裝所使用的 R 工具的執行個體使用 > 確定要使用的執行個體相關聯的 R 程式庫。

下列章節提供有關如何管理封裝的其他詳細資料使用這兩個選項來執行。

## <a name="r-package-management-using-t-sql"></a>使用 T-SQL 的 R 封裝管理

SQL Server 2017 包含新的 T-SQL 陳述式讓 DBA 更充分掌控資料庫層級的 R 封裝。 同時，DBA 可以讓使用者能夠安裝的套件的必要且與他人共用。

如果您需要與他人共用封裝，或如果多位人員需要在伺服器上執行機器學習工作，建議您啟用封裝管理，將使用者指派至資料庫角色，並上傳封裝，讓使用者可以共用它們。

在 SQL Server 2017 封裝管理會依賴這些新的資料庫物件和功能：

+ 新的資料庫角色，來管理封裝的存取和使用
+ 封裝範圍，另一個共用和私用套件
+ 建立外部程式庫的陳述式中上, 傳到伺服器的新程式碼程式庫
+ 新的 R 函數 RevoScaleR，以支援 SQL Server 中的安裝封裝中計算內容
+ 封裝的同步處理，以確保輕鬆備份和還原封裝

### <a name="database-roles-for-package-management"></a>用於封裝管理的資料庫角色

資料庫管理員必須建立用於封裝管理述這裡執行的指令碼的角色：[啟用或停用封裝管理](r-package-how-to-enable-or-disable.md)。

執行這個指令碼之後，您應該會看到下列新的資料庫角色：

+ `rpkgs-users`： 此角色的成員可以使用另一個已安裝任何共用的封裝`rpkgs-shared`角色成員。

+ `rpkgs-private`： 此角色的成員有共用封裝，做為成員的相同的權限的存取權`rpkgs-users`角色。 此角色的成員也可以安裝、 移除和使用非公開已設定領域的封裝。

+ `rpkgs-shared`： 此角色的成員具有相同的權限的成員`rpkgs-private`角色。 此外，此角色的成員可以安裝或移除共用的封裝。

+ `db_owner`： 此角色的成員具有相同的權限的成員`rpkgs-shared`角色。 此外，此角色的成員可以**授與**其他使用者的權限安裝或移除兩者共用和私用的封裝。

DBA 會將使用者加入至每個資料庫為基礎來控制使用者的能力來安裝封裝的角色。

### <a name="package-scope"></a>封裝範圍

新的封裝管理功能來它們是私用，或是可由多個使用者共用區分封裝。

+ **共用範圍**

    *共用範圍*表示具有共用的範圍角色的權限之使用者 (`rpkgs-shared`) 可以安裝和解除安裝指定的資料庫中的封裝。 安裝在共用範圍中的封裝可供 SQL Server 資料庫的其他使用者使用，但前提是這些使用者可以使用已安裝的 R 封裝。

+ **私用範圍**

    *私用範圍*表示使用者已經提供成員資格的私用範圍的角色 (`rpkgs-private`) 可以安裝或解除封裝安裝到每個使用者定義的私用程式庫位置。 因此，安裝在私用範圍中的任何封裝只能供安裝的使用者使用。 換句話說，SQL Server 上的使用者無法使用其他使用者所安裝的私用封裝。

您可以結合這些「共用」  和「私用」  範圍模型，開發可在 SQL Server 上部署和管理封裝的自訂安全系統。

例如，藉由使用共用範圍，可授與資料科學家群組的負責人或管理員安裝封裝的權限，這些封裝接著可供相同 SQL Server 執行個體中的所有其他使用者或資料科學家使用。

另一種情況可能需要提高使用者之間的隔離，或使用不同版本的封裝。 在此情況下，負責只安裝和使用所需封裝的資料科學家，可透過私用範圍來取得個別權限。 由於這些封裝是針對每位使用者所安裝，因此某位使用者所安裝的封裝不會影響使用相同 SQL Server 資料庫之其他使用者的工作。

### <a name="create-external-library"></a>建立外部程式庫

[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)是可協助資料庫管理員，而不需要使用者 R 工具處理封裝的 SQL Server 2017 中導入新的 T-SQL 陳述式。 

您使用**建立外部程式庫**陳述式來將外部程式庫上傳至 zip 的檔案格式中的執行個體。 授權的使用者可以存取文件庫，並安裝，以供自己使用。

例如，您可以建立您的 R 專案，每個不同版本的多個複本。 將其上傳做為個別的程式庫，可讓您保留某些版本的私用，並與其他使用者共用某些版本。

「 媒體櫃 」 基本上是您想要讓使用者以單一名稱使用的外部封裝的集合。 比方說，您可能會發行下列任一項到 SQL Server 做為外部程式庫：

+ 單一的 R 封裝，您所撰寫，不含相依性
+ 您想要安裝封裝和安裝所需的相依性
+ 與特定工作或專案中，與它們的相依性的 R 封裝的集合

程式庫名稱是用來管理封裝或 SQL Server 中的封裝的集合，而且可以是獨立的安裝套件。 不過，程式庫名稱必須是唯一的整個執行個體。

若要使用此陳述式，封裝管理功能必須啟用執行個體上。 如需詳細資訊，請參閱[建立外部程式庫](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

> [!NOTE]
> 目前您可以使用此陳述式，可以建立僅以 Windows 為基礎的文件庫，針對 r 支援已規劃未來的 Python 封裝，以及在其他平台，例如 Linux 執行的封裝。

外部程式庫已上傳到伺服器之後，您必須安裝執行個體相關聯的 R 封裝程式庫。 有數種方式來執行這項操作：

+ 執行標準 R 命令`install.packages`sp_execute_external_script 內。 請務必使用具有權限才能安裝封裝的帳戶進行連接。

+ 從遠端的 R 用戶端連接到 SQL Server 和執行[rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) SQL Server 計算內容中。 同樣地，您必須具有權限才能安裝封裝在私用或共用的範圍內，若要這樣做。

若要查看使用 R 和 T-SQL 安裝範例，請參閱[SQL Server 上安裝其他封裝](install-additional-r-packages-on-sql-server.md)。

### <a name="new-r-functions-for-package-installation"></a>封裝安裝新的 R 函數

已啟用封裝管理的資料庫角色之後，使用者也可以使用新的函式中[ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)指定為 SQL Server 計算內容執行個體上安裝的封裝。

+ 資料科學家可以安裝 SQL Server 上所需的 R 封裝，而不需要直接存取 SQL Server 電腦。

+ 使用者可以安裝封裝，並與他人共用安裝的套件共用的範圍。 然後相同的 SQL Server 資料庫的其他授權的使用者可以存取封裝。

+ 使用者可以安裝不會顯示給其他人的私人封裝建立 R 封裝的私用沙箱。

RevoScaleR，提供下列封裝管理功能的安裝與移除指定的計算內容中的封裝：

-   [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages)： 尋找指定的計算內容中安裝套件的相關資訊。

-   [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages)： 安裝封裝到計算內容中，從指定的儲存機制，或藉由讀取本機儲存壓縮封裝。

-   [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages)： 移除計算內容從安裝套件。

-   [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage)： 取得指定的計算內容中的一個或多個封裝的路徑。

-   [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)： 在指定的計算內容中複製封裝程式庫檔案系統與資料庫之間。

-   [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths)： 在 SQL Server 內執行時取得封裝程式庫的樹狀目錄的搜尋路徑。

若要使用這些函式，連接到 SQL Server 具有必要的權限，使用 SQL Server 計算內容執行個體。 當您連線時，您的認證會決定是否可以在伺服器上完成作業。

封裝安裝函數會檢查相依性，並確保所有相關的封裝都會安裝至 SQL Server，就像是本機計算內容中的 R 封裝安裝一樣。 解除安裝封裝的函數也會計算相依性，並確保移除 SQL Server 上的其他封裝不再使用的封裝，以便釋出資源。

> [!NOTE]
> 
> 根據預設，在 SQL Server 2017 包括這些新的函式。 您可以更新，以取得這些函式執行個體升級為使用較新版的 Microsoft R Server，例如 Microsoft R Server 9.0.1 RevoScaleR 版本。
> 
> 如需詳細資訊，請參閱[使用 SqlBindR.exe 至 upgradeR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

### <a name="synchronization-of-r-package-libraries"></a>同步處理的 R 封裝程式庫

CTP 2.0 版本的 SQL Server 2017 （和 Microsoft R Server 2017 年 4 月發行） 包含新的 R 函數，如*同步處理封裝*。

封裝的同步處理表示 database engine 會追蹤由特定擁有者和群組，並視需要將這些封裝寫入數個檔案系統的封裝。 在這些情況下，您可以使用封裝的同步處理：

+ 您想要 SQL Server 執行個體之間移動的 R 封裝。
+ 您需要重新安裝套件的特定使用者或群組之後還原資料庫。

如需如何啟用和使用這項功能的詳細資訊，請參閱[R 封裝的同步處理 SQL server](package-install-uninstall-and-sync.md)。

## <a name="r-package-management-using-traditional-r-tools"></a>使用傳統的 R 工具的 R 封裝管理

管理 R 封裝的執行個體上的傳統方法是安裝，並列出封裝使用的 R 工具和命令。 

+ 如果您使用 SQL Server 2016 的早期版本，此選項可能是唯一的選項。  
+ 如果您的 R 封裝的唯一使用者，且有系統管理伺服器的存取權，此選項可能也會很方便。
+ 若要簡化管理的 R 封裝版本，您可以使用[miniCRAN](create-a-local-package-repository-using-minicran.md)來建立本機儲存機制和的執行個體之間共用。

如需詳細資訊，請參閱下列文章：

+ [SQL Server 上安裝其他的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [決定要安裝在 SQL Server 上的套件](determine-which-packages-are-installed-on-sql-server.md)

SQL Server 2017，我們建議您使用建立外部程式庫並管理使用者和他們的 R 封裝提供的資料庫角色。

## <a name="next-steps"></a>後續的步驟

[如何啟用或停用的 R 封裝管理](../r/r-package-how-to-enable-or-disable.md)
