---
title: 使用 R 套件管理員
description: 使用如安裝套件等標準 R 命令，以將新的 R 套件新增至 SQL Server 2016 R Services 或 SQL Server Machine Learning Services (資料庫內)。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f6d828a7267ab2b4b1def17f9d1c6bf4a6018dc
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633612"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>使用 R 套件管理員在 SQL Server 上安裝 R 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

您可以使用標準 R 工具，以在 SQL Server 2016 或 SQL Server 2017 的執行個體上安裝新的套件，並將開啟連接埠 80 提供給該電腦，而且您擁有系統管理員許可權。

> [!IMPORTANT] 
> 請務必將套件安裝到與目前執行個體關聯的預設程式庫， 永遠不要將套件安裝到使用者目錄。

此程序會使用 RGui，但您也可以使用 RTerm 或任何其他支援已提升存取權的 R 命令列工具。

## <a name="install-a-package-using-rgui"></a>使用 Rgui 來安裝套件

1. [找到執行個體程式庫的位置](../package-management/r-package-information.md)， 並導覽至已安裝 R 工具的資料夾。 例如，SQL Server 2017 預設執行個體的預設路徑為：`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. 以滑鼠右鍵按一下 [RGui.exe]，然後選取 [以系統管理員身分執行]  。 如果您沒有必要的許可權，請洽詢資料庫管理員，並提供您所需的套件清單。

1. 如果您知道套件名稱，您可以在命令列中輸入：`install.packages("the_package-name")`，套件名稱一律使用雙引號。

1. 如果需要您提供鏡像網站，請選取對您位置而言方便的任意鏡像網站。

如果目標套件相依於其他套件，R 安裝程式就會為您自動下載相依性並安裝。

如果您有多個 SQL Server 執行個體 (例如 SQL Server 2016 R 服務和 SQL Server 機器學習服務的並排執行個體)，而您想要在這兩個內容中使用套件，請個別安裝每個執行個體。 因為套件無法跨執行個體共用。

## <a name = "bkmk_offlineInstall"></a> 使用 R 工具進行離線安裝

如果伺服器無法存取網際網路，則需要額外的步驟來準備套件。 若要在無法存取網際網路的伺服器上安裝 R 套件，您必須：

+ 事先分析相依性。
+ 將目標套件下載到具有網際網路存取的電腦。
+ 將所有必要的套件下載至同一部電腦，並將所有套件放在單一套件封存中。
+ 如果該封存還不是 ZIP 壓縮格式，請將其壓縮。
+ 將套件封存複製到伺服器上的位置。
+ 安裝將封存檔案指定為來源的目標套件。

> [!IMPORTANT] 
>  在您開始安裝「**之前**」，請務必分析所有相依性，並下載「**所有**」必要套件。 我們建議您在此流程中使用 [miniCRAN](https://mran.microsoft.com/package/miniCRAN)。 您可以提供想要安裝的套件清單給此 R 套件，使其分析相依性，並為您取得所有 ZIP 壓縮檔案， 接著 miniCRAN 會建立一個單一存放庫，您可以將此存放庫複製到伺服器電腦中。 如需詳細資訊，請參閱[使用 miniCRAN 建立本機套件存放庫](create-a-local-package-repository-using-minicran.md)

此程序是以您已備妥所需的所有套件 (ZIP 壓縮格式)，並且已準備好將其複製到伺服器為前提。

1. 將套件 ZIP 壓縮檔案或多個套件 (包含了所有 ZIP 壓縮格式套件的完整存放庫) 複製到伺服器可以存取的位置。

2. 開啟安裝了針對執行個體之 R 工具的伺服器上的資料夾。 例如，如果您在具有 SQL Server 2016 R 服務的系統上使用 Windows 命令提示字元，請切換至 `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 在 [RGui] 或 [RTerm] 上按一下滑鼠右鍵，然後選取 [以系統管理員身分執行]  。

4. 執行 R 命令 `install.packages`，並指定套件或存放庫名稱，以及 ZIP 壓縮檔案 的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    這個命令會從本機 ZIP 壓縮檔案解壓縮 R 套件 `mynewpackage` (假設您的複本已儲存在目錄 `C:\Temp\Downloaded packages`，並且將套件安裝於本機電腦)。 如果套件有任何相依性，安裝程式則會檢查程式庫中的現有套件。 如果您已建立包含相依性的存放庫，安裝程式也會安裝必要的套件。

    如果執行個體程式庫中沒有任何必要的套件，而且在 ZIP 壓縮檔案中找不到，則目標套件的安裝會失敗。

## <a name="see-also"></a>另請參閱

+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)
