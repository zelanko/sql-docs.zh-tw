---
title: "SQL Server 的 R 封裝管理 |Microsoft 文件"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 576178e53a28f877ac91d99f14ce9ba6a44e506d
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="r-package-management-for-sql-server"></a>SQL Server 的 R 封裝管理

本文說明 R 封裝和 SQL Server 2016 中 SQL Server 2017 的管理的功能。

+ 管理 R 封裝 （和 Python 封裝） 的建議的方法
+ SQL Server 2016 和 2017年之間的封裝管理中的變更

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務

## <a name="recommended-methods-for-package-management"></a>封裝管理的建議的方法

在 SQL Server 2016 和 SQL Server 2017，電腦的系統管理員可以安裝每個執行個體已啟用機器學習的封裝。 

封裝會安裝到檔案系統中，使用執行個體的程式庫，和不在執行個體之間共用。 這是目前的 SQL Server 2016 和 SQL Server 2017 的建議的方法。

+ [SQL Server 上安裝其他的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [決定要安裝在 SQL Server 上的套件](determine-which-packages-are-installed-on-sql-server.md)

此外，如果您有**dbo**角色成員資格上已啟用機器學習的 SQL Server 執行個體，您可以安裝 R 封裝從遠端用戶端，使用 RevoScaleR 中的新函式。

+ [封裝安裝新的 R 函數](#bkmk_remoteInstall)

### <a name="installation-on-servers-with-no-internet-access"></a>在沒有網際網路存取的伺服器上安裝

若要讓您更輕鬆地判斷所需的 R 封裝版本，並提供所有套件相依性，您可以使用[miniCRAN](https://mran.microsoft.com/package/miniCRAN)。 此 R 封裝為目標的封裝的清單，並建立包含目標封裝以及所有其相依性，以壓縮格式的本機儲存機制。 然後，您可以將之複製到離線的伺服器，或共用多個執行個體之間的儲存機制。

如需詳細資訊，請參閱[建立本機封裝儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)。

### <a name="python-packages"></a>Python 封裝

安裝新的 Python 封裝會遵循相同的指導方針： 

+ 檢閱預先來判斷與目前的 Python 版本的相容性的 Python 封裝
+ 評估 Python 封裝適合強行寫入的 SQL Server 環境
+ 使用系統管理員身分安裝封裝的 Python 工具
+ 安裝必須只能在執行個體文件庫中的 SQL Server 內容中執行的封裝。 
+ 如果您使用多個環境進行測試時，生產環境，以此類推，請確定相同版本的 Python 封裝已安裝執行個體文件庫中。

如需安裝步驟，請參閱[SQL Server 上安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)

## <a name="features-for-package-management-in-sql-server-2016-and-sql-server-2017"></a>在 SQL Server 2016 和 SQL Server 2017 封裝管理功能

SQL Server 2017 加入一些新功能，可支援的 R （及 Python） 由資料庫管理員的封裝更容易管理。 這些新功能包括：

+ 安裝或管理封裝使用 T-SQL 的文件庫的能力
+ 資料庫層級透過資料庫角色的使用者權限管理。 

在未來版本中，這些功能應該要提供由資料庫管理員的封裝管理的主要方法，並簡化資料科學家安裝所需的程式庫。

在同一時間，Microsoft R Server 和機器學習伺服器加入新的 R 函數，可以更輕鬆地安裝和共用的 SQL Server 計算內容中的封裝。 這些函數與根據 T-SQL 的 SQL Server 功能分開運作，並要從遠端的 R 用戶端執行。

本節提供這些功能的概觀。

### <a name="bkmk_remoteInstall"></a>封裝安裝新的 RevoScaleR 函式 

為最新版本的 R 伺服器或機器學習服務伺服器的使用者也可以使用新的函式中[ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)指定為 SQL Server 計算內容執行個體上安裝的封裝。

+ 資料科學家可以安裝 SQL Server 上所需的 R 封裝，而不需要直接存取 SQL Server 電腦。 不過，使用者必須是資料庫擁有者的成員 (**dbo**) 角色。

+ 使用者可以共用封裝與他人共用範圍隨安裝套件。 相同的 SQL Server 資料庫的其他授權的使用者可以存取封裝。

+ 使用者可以安裝不會顯示給其他人的私人封裝建立 R 封裝的私用沙箱。

+ 輕鬆備份和還原封裝，可讓封裝同步處理

#### <a name="package-installation-functions"></a>封裝安裝函式

RevoScaleR，提供下列封裝管理功能的安裝與移除指定的計算內容中的封裝：

-   [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages)： 尋找指定的計算內容中安裝套件的相關資訊。

-   [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)： 安裝封裝到計算內容中，從指定的儲存機制，或藉由讀取本機儲存壓縮封裝。

-   [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages)： 移除計算內容從安裝套件。

-   [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage)： 取得指定的計算內容中的一個或多個封裝的路徑。

-   [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages)： 在指定的計算內容中複製封裝程式庫檔案系統與資料庫之間。

-   [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)： 在 SQL Server 內執行時取得封裝程式庫的樹狀目錄的搜尋路徑。

若要使用這些函式，連接到 SQL Server 具有必要的權限，使用 SQL Server 計算內容執行個體。 

> [!IMPORTANT]
> 您在連接中使用的認證會決定是否可以在伺服器上完成作業。

這些封裝安裝函式相依性檢查，並確保任何相關的封裝可以安裝到 SQL Server，就像在本機計算內容中的 R 封裝安裝。 解除安裝封裝的函數也會計算相依性，並確保移除 SQL Server 上的其他封裝不再使用的封裝，以便釋出資源。

這些新的函式會包含在安裝在 SQL Server 2017 的 RevoScaleR 的版本。 您也可以取得這些函式[升級 SQL Server 執行個體](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)使用最近版本[Microsoft R Server 或機器學習 Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)。 需要 9.0.1 版或更新版本。

#### <a name="package-synchronization-functions"></a>封裝的同步處理函式

封裝的同步處理是僅限 R 封裝的新功能。 Database engine 會追蹤由特定擁有者和群組，並視需要將這些封裝寫入數個檔案系統的封裝。 一般而言，您可在這些案例中使用封裝同步處理：

+ 您想要 SQL Server 執行個體之間移動的 R 封裝。
+ 您需要重新安裝套件的特定使用者或群組之後還原資料庫。

如需如何啟用和使用這項功能的詳細資訊，請參閱[R 封裝的同步處理 SQL server](package-install-uninstall-and-sync.md)。

### <a name="package-management-using-t-sql"></a>使用 T-SQL 的封裝管理

SQL Server 2017 加入新的 T-SQL 陳述式，以讓 DBA 更充分掌控資料庫層級的 R 封裝。 DBA 應該不需要了解如何使用 R 或 Python tools，但改為應該要能夠讓 R 或 Python 使用者能夠安裝必要且與他人共用的封裝。

這項功能是在多使用者環境中進行共同作業和版本管理更容易： 例如：

+ 您想要共用已與其他人在您的小組開發的封裝。
+ 多個分析師使用相同的資料庫中，而且需要使用不同版本的相同的封裝。
+ 您想要移動資料庫，或當您執行備份和還原作業的同時移動封裝和其權限。

在 SQL Server 2017 封裝管理會依賴這些新的資料庫物件和功能：

+ [新的資料庫角色](#bkmk_roles)、 管理封裝的存取和使用
+ [建立外部程式庫](#bkmk_createExternalLibrary)陳述式中上, 傳到伺服器的封裝程式庫

使用這些功能會需要一些額外的準備工作執行個體和資料庫層級： 

+  資料庫管理員必須明確啟用封裝管理功能執行指令碼會建立必要資料庫物件。 如需詳細資訊，請參閱[如何啟用 R 封裝管理](r-package-how-to-enable-or-disable.md)。

+ 使用者必須被指派至角色，每個資料庫層級上。 這些角色可讓使用者安裝共用或私用的封裝。

+ 可以使用新的 T-SQL 陳述式，建立外部程式庫來安裝封裝程式庫。 不過，所有套件相依性必須事先準備好，並安裝為單一的壓縮檔的一部分。

> [!NOTE]
> 雖然此時，此處所述的功能可完全正常運作，未來的版本會包含其他的增強功能，讓它更容易準備封裝程式庫，以及管理相依性。 如果您熟悉以 R 封裝安裝時，我們建議您繼續使用目前的 R 工具。

#### <a name="bkmk_createExternalLibrary"></a>建立外部程式庫 

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

為了確保提供所有套件相依性，我們建議您使用[miniCRAN](create-a-local-package-repository-using-minicran.md)建立本機儲存機制。 您接著可以使用該 zip 壓縮的檔案安裝目標封裝和其相依性。

#### <a name="bkmk_roles"></a>封裝管理的資料庫角色 

根據預設，即使在執行個體，其中已安裝並啟用機器學習中不包含新的封裝管理 SQL Server 中提供的角色。 您必須將角色加入述這裡執行的指令碼：[啟用或停用封裝管理](r-package-how-to-enable-or-disable.md)。

執行這個指令碼之後，您應該會看到下列新的資料庫角色：

+ `rpkgs-users`： 此角色的成員可以使用另一個已安裝任何共用的封裝`rpkgs-shared`角色成員。

+ `rpkgs-private`： 此角色的成員有共用封裝，做為成員的相同的權限的存取權`rpkgs-users`角色。 此角色的成員也可以安裝、 移除和使用非公開已設定領域的封裝。

+ `rpkgs-shared`： 此角色的成員具有相同的權限的成員`rpkgs-private`角色。 此外，此角色的成員可以安裝或移除共用的封裝。

+ `db_owner`： 此角色的成員具有相同的權限的成員`rpkgs-shared`角色。 此外，此角色的成員可以**授與**其他使用者的權限安裝或移除兩者共用和私用的封裝。

DBA 可以將使用者新增至每個資料庫為基礎的角色。



## <a name="next-steps"></a>後續步驟

[SQL Server 機器學習的封裝管理](r-package-management-for-sql-server-r-services.md)