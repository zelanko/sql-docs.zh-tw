---
title: 使用 R 套件管理員 SQL Server Machine Learning 服務
description: 使用標準的 R 命令，例如 install.packages 將新的 R 套件新增至 SQL Server 2016 R Services 或 SQL Server 2017 Machine Learning 服務 （資料庫）。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2582d519893fac3a49ce997674980d2d58d5cf32
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140782"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>使用 SQL Server 上安裝 R 套件的 R 套件管理員
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

您可以使用標準 R 工具的 SQL Server 2016 執行個體上安裝新的封裝或 SQL Server 2017 中，提供在電腦已開啟的連接埠 80 和有系統管理員權限。

> [!IMPORTANT] 
> 請務必將封裝安裝到目前的執行個體相關聯的預設程式庫。 永遠不會將套件安裝至使用者目錄。

此程序使用 RGui，但您可以使用 RTerm 或任何其他 R 命令列工具，可支援高的存取權限。

## <a name="install-a-package-using-rgui"></a>使用 RGui 安裝封裝

1. [判斷執行個體文件庫的位置](../package-management/default-packages.md)。 瀏覽至安裝 R 工具的資料夾。 例如，SQL Server 2017 的預設執行個體的預設路徑如下所示： `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. 以滑鼠右鍵按一下 RGui.exe，然後選取**系統管理員身分執行**。 如果您沒有必要的權限，請連絡資料庫管理員，並提供所需的套件清單。

1. 從命令列中，如果您知道封裝名稱，您可以輸入：`install.packages("the_package-name")` 雙引號是必要的封裝名稱。

1. 當系統要求您的鏡像網站，選取 是方便您位置的任何網站。

如果目標封裝相依於其他封裝，R 安裝程式自動下載的相依性，並會為您安裝它們。

如果您有多個執行個體的 SQL Server，並排顯示執行個體的 SQL Server 2016 R Services 和 SQL Server 2017 Machine Learning 服務，例如執行分別為每個執行個體的安裝，如果您想要使用這兩種內容中的封裝。 封裝無法執行個體之間共用。

## <a name = "bkmk_offlineInstall"></a> 使用 R 工具的離線安裝

如果伺服器沒有網際網路存取，額外的步驟，才能準備封裝。 若沒有網際網路存取的伺服器上安裝 R 封裝，您必須：

+ 事先分析相依性。
+ 目標套件下載至具有網際網路存取的電腦。
+ 任何必要的套件下載到同一部電腦，並將所有的套件放置在單一封裝的保存。
+ 如果它尚未以壓縮格式的 zip 封存。
+ 將套件封存檔複製到伺服器上的位置。
+ 安裝目標套件指定為來源封存檔案。

> [!IMPORTANT] 
>  請務必讓您分析所有的相依性，並下載**所有**必要封裝**之前**開始安裝。 我們建議[miniCRAN](https://mran.microsoft.com/package/miniCRAN)此處理程序。 此 R 封裝會使用您想要安裝、 分析相依性，以及為您取得所有壓縮的檔案的封裝清單。 miniCRAN 接著會建立單一的存放庫，您可以複製到伺服器電腦上。 如需詳細資訊，請參閱[建立本機套件儲存機制使用 miniCRAN](create-a-local-package-repository-using-minicran.md)

此程序假設您已備妥您需要以壓縮格式，並已準備好將它們複製到伺服器的所有封裝。

1. 複製封裝壓縮檔案，或多個封裝，如完整的存放庫包含中的所有封裝壓縮格式，伺服器可以存取的位置。

2. 開啟伺服器上安裝 R 工具的執行個體所在的資料夾。 例如，如果您在 SQL Server 2016 R Services 的系統上使用 Windows 命令提示字元，切換至`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 以滑鼠右鍵按一下 RGui 或 RTerm，然後選取**系統管理員身分執行**。

4. 執行 R 命令`install.packages`並指定封裝或存放庫名稱和壓縮檔案的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令會解壓縮 R 封裝`mynewpackage`從其本機 zip 壓縮檔，假設您的複本儲存在目錄中`C:\Temp\Downloaded packages`，並在本機電腦上安裝套件。 如果封裝有任何相依性，安裝程式會檢查文件庫中現有的封裝。 如果您已建立的存放庫，包含相依性，則安裝程式會安裝所需的套件。

    如果任何必要的套件不會出現在執行個體文件庫中，和在 zip 檔案中找不到，安裝目標套件將會失敗。

## <a name="see-also"></a>另請參閱

+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)
