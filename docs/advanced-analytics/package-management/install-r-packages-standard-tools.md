---
title: 使用 R 工具來安裝套件
description: 了解如何使用標準 R 工具，在 SQL Server 機器學習服務或 SQL Server R Services 的執行個體上安裝新的 R 套件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/20/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 5d7c610f887de137c44f97ca8809e70c548a51db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74485313"
---
# <a name="install-packages-with-r-tools"></a>使用 R 工具來安裝套件

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此文章說明如何使用標準 R 工具，在 SQL Server 機器學習服務或 SQL Server R Services 的執行個體上安裝新的 R 套件。 您可以將套件安裝在有網際網路連線以及與網際網路隔離的 SQL Server 上。

除了標準的 R 工具以外，您也可以使用以下工具安裝 R 套件：

+ [RevoScaleR](install-r-packages-with-revoscaler.md)
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
+ [T-SQL](install-r-packages-with-tsql.md) (CREATE EXTERNAL LIBRARY)
::: moniker-end

## <a name="general-considerations"></a>一般考量

+ 在 SQL Server 中執行的 R 程式碼只能使用安裝在預設執行個體程式庫中的套件。 SQL Server 無法從外部程式庫載入套件，即使該程式庫位於相同電腦上也一樣。
這包括隨其他 Microsoft 產品安裝的 R 程式庫。

+ R 套件程式庫位於 SQL Server 執行個體的 Program Files 資料夾中，而且根據預設，在此資料夾中安裝需要系統管理員權限。 如需詳細資訊，請參閱[套件程式庫位置](../package-management/r-package-information.md#default-r-library-location)。

  ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
  非系統管理員可以使用 RevoScaleR 9.0.1 與更新版本，或使用 CREATE EXTERNAL LIBRARY 來安裝套件。 **dbo_owner** 使用者，或具有 CREATE EXTERNAL LIBRARY 權限的使用者，可以將 R 套件安裝到目前的資料庫。 如需詳細資訊，請參閱
  + [使用 RevoScaleR 來安裝 R 套件](install-r-packages-with-revoscaler.md)
  + [使用 T-SQL (CREATE EXTERNAL LIBRARY) 在 SQL Server 上安裝 R 套件](install-r-packages-with-tsql.md)
  ::: moniker-end

  ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  非系統管理員可以使用 RevoScaleR 9.0.1 與更新版本來安裝套件。 **dbo_owner** 使用者可以將 R 套件安裝到目前的資料庫。 如需詳細資訊，請參閱[使用 RevoScaleR 來安裝 R 套件](install-r-packages-with-revoscaler.md)。
  ::: moniker-end

+ 在已強化的 SQL Server 環境中，您可以避免下列情況：
  + 需要網路存取的套件
  + 需要提升檔案系統存取權的套件
  + 用於網頁程式開發或其他工作，但無法透過在 SQL Server 內部執行而獲益的套件

## <a name="online-installation-with-internet-access"></a>線上安裝 (具有網際網路存取)

如果 SQL Server 可存取網際網路，您就可以使用標準套件安裝工具來安裝 R 套件。

1. 判斷執行個體程式庫的位置 (請參閱[取得 R 套件資訊](../package-management/r-package-information.md))，並瀏覽至 R 工具安裝所在的資料夾。

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   例如，SQL Server 預設執行個體的預設路徑為：

   `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   例如，SQL Server 預設執行個體的預設路徑為：

   `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

1. 以系統管理員身分從這個資料夾執行 **R** 或 **Rgui**。

1. 執行 R 命令 `install.packages` 並指定套件名稱。 如果套件具有任何相依性，安裝程式會自動下載並安裝相依性。

如果您有多個並行的 SQL Server 執行個體，請針對您要使用套件的每個執行個體個別執行安裝作業。 因為套件無法跨執行個體共用。

## <a name = "bkmk_offlineInstall"></a> 離線安裝 (無網際網路存取)

裝載生產資料庫的伺服器通常不會有網際網路連線。 若要在該環境中安裝 R 套件，您可以先下載並準備套件與相依性 (壓縮檔案形式)，然後將檔案複製到伺服器上的資料夾。 檔案備妥之後，即可離線安裝套件。

識別所有相依性會變得很複雜。 針對 R，建議您使用 [**miniCRAN**](https://andrie.github.io/miniCRAN/) 來建立本機存放庫。
您可以提供要安裝套件的清單給 **miniCRAN**，讓其分析相依性，以及收集所有必要的壓縮檔案。 接著，該工具會建立單一存放庫，您可以將其複製到隔離的 SQL Server 執行個體。 [**igraph**](https://igraph.org/r/) 套件在分析套件相依性方面也很有幫助。

如需詳細資訊，請參閱[使用 miniCRAN 建立本機 R 套件存放庫](create-a-local-package-repository-using-minicran.md)。

在 ZIP 檔案位於 SQL Server 執行個體上之後，您就可以在伺服器上使用標準 R 工具加以安裝。

1. 判斷執行個體程式庫的位置 (請參閱[取得 R 套件資訊](../package-management/r-package-information.md))，並瀏覽至 R 工具安裝所在的資料夾。 

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   例如，SQL Server 預設執行個體的預設路徑為：

   `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   例如，SQL Server 預設執行個體的預設路徑為：

   `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

1. 以系統管理員身分從這個資料夾執行 **R** 或 **Rgui**。

1. 執行 R 命令 `install.packages`，並指定套件或存放庫名稱，以及 ZIP 壓縮檔案 的位置。 例如：

   ```R
   install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
   ```

   此命令會從本機壓縮檔案將 R 套件 `mynewpackage` 解壓縮，然後安裝套件。 如果套件有任何相依性，安裝程式則會檢查程式庫中的現有套件。 如果您已建立包含相依性的存放庫，安裝程式也會安裝必要的套件。

   > [!NOTE]
   > 如果執行個體程式庫中沒有任何必要的套件，而且在 ZIP 壓縮檔案中找不到，則目標套件的安裝會失敗。

您也可以不使用 **miniCRAN**，改為手動執行下列步驟：

1. 識別所有套件相依性。
1. 檢查伺服器上是否已安裝任何必要套件。 如果已安裝套件，請確認版本正確無誤。
1. 將套件與所有相依性下載到具備網際網路存取權的個別電腦。
1. 將套件與相依性放在單一套件封存中。
1. 如果該封存還不是壓縮格式，請將其壓縮。
1. 將檔案移到伺服器可存取的資料夾。
1. 執行支援的安裝命令或 DDL 陳述式，將套件安裝至執行個體程式庫。

## <a name="see-also"></a>另請參閱

+ [取得 R 套件資訊](r-package-information.md)
+ [使用 R 套件的祕訣](tips-for-using-r-packages.md)
+ [SQL Server R 語言教學課程](../tutorials/sql-server-r-tutorials.md)
