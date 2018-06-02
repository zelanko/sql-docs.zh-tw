---
title: SQL Server 機器學習服務上安裝新的 R 封裝 |Microsoft 文件
description: 將新的 R 封裝加入至 SQL Server 2016 R Services 或 SQL Server 2017 機器學習服務 （資料庫）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8f7b0ee2b623f6a208a92823948bf0295bae33f6
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707496"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>若要在 SQL Server 上安裝 R 封裝中使用 R 封裝管理員
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

您可以使用標準的 R 工具來安裝新的封裝上的 SQL Server 2016 執行個體或 SQL Server 2017，提供在電腦已開啟的連接埠 80，並可讓系統管理員權限。

> [!IMPORTANT] 
> 請務必要與目前的執行個體相關聯的預設文件庫安裝封裝。 永遠不會安裝到使用者目錄的封裝。

此程序使用 RGui，但您可以使用 RTerm 或任何其他 R 命令列工具，可支援高的存取權限。

## <a name="install-a-package-using-rgui"></a>使用 RGui 安裝封裝

1. [判斷執行個體文件庫的位置](installing-and-managing-r-packages.md)。 瀏覽至安裝 R 工具的資料夾。 例如，SQL Server 2017 預設執行個體的預設路徑如下所示： `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. 以滑鼠右鍵按一下 RGui.exe，然後選取**系統管理員身分執行**。 如果您沒有必要的權限，請連絡資料庫管理員，並提供您需要的套件清單。

1. 從命令列中，如果您知道封裝名稱，您可以輸入：`install.packages("the_package-name")`雙引號所需的封裝名稱。

1. 當系統要求您的鏡像網站，選取對您位置而言方便的任何網站。

如果目標封裝相依於其他封裝，R 安裝程式會自動下載相依性，並讓您將進行安裝。

如果您有多個執行個體的 SQL Server，並存的執行個體的 SQL Server 2016 R 服務和 SQL Server 2017 機器學習服務，例如執行分別為每個執行個體的安裝，如果您想要使用這兩種內容中的封裝。 封裝無法執行個體之間共用。

## <a name = "bkmk_offlineInstall"></a> 使用的 R 工具的離線安裝

如果伺服器沒有網際網路存取，不需要其他步驟以準備封裝。 若要在沒有網際網路存取的伺服器上安裝 R 封裝，您必須：

+ 事先分析相依性。
+ 目標套件下載至具有網際網路存取的電腦。
+ 相同的電腦下載任何所需的封裝，並將所有封裝都放在單一封裝的保存。
+ 如果它尚未以壓縮格式，zip 封存。
+ 將套件保存複製到伺服器上的位置。
+ 安裝目標封裝封存檔案指定為來源。

> [!IMPORTANT] 
>  確定您分析所有相依性，並下載**所有**所需封裝**之前**開始安裝。 我們建議[miniCRAN](https://mran.microsoft.com/package/miniCRAN)此處理程序。 此 R 封裝會採用您想要安裝、 分析相依性，以及讓您取得所有 zip 的檔案的封裝清單。 miniCRAN 接著會建立單一的存放庫，您可以複製到伺服器電腦。 如需詳細資訊，請參閱[建立使用 miniCRAN 本機封裝儲存機制](create-a-local-package-repository-using-minicran.md)

此程序假設您已經備妥您需要以壓縮格式，並準備好將它們複製到伺服器的所有封裝。

1. 複製封裝壓縮檔案，或多個封裝，完整的儲存機制包含中的所有封裝壓縮格式，伺服器可以存取的位置。

2. 開啟伺服器上安裝 R 工具的執行個體所在的資料夾。 例如，如果您使用 SQL Server 2016 R Services 的系統上的 Windows 命令提示字元，切換至`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 以滑鼠右鍵按一下 RGui 或 RTerm，然後選取**系統管理員身分執行**。

4. 執行 R 指令`install.packages`並指定封裝或儲存機制名稱和壓縮檔案的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令會擷取 R 封裝`mynewpackage`從其本機的 zip 檔案，假設您的複本儲存在目錄中`C:\Temp\Downloaded packages`，並在本機電腦上安裝封裝。 如果封裝有任何相依性，安裝程式會檢查文件庫中現有的封裝。 如果您已經建立包含相依性的儲存機制，安裝程式會安裝必要的封裝。

    如果任何必要的封裝不會出現在執行個體文件庫，zip 檔案中找不到目標套件的安裝將會失敗。

## <a name="see-also"></a>另請參閱

+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)