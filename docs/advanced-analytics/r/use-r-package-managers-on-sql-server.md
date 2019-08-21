---
title: 使用 R 套件管理員
description: 使用如 install 等標準 R 命令, 將新的 R 封裝新增至 SQL Server 2016 R Services 或 SQL Server Machine Learning Services (資料庫內)。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f6d828a7267ab2b4b1def17f9d1c6bf4a6018dc
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633612"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>使用 R 套件管理員在 SQL Server 上安裝 R 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

您可以使用標準 R 工具, 在 SQL Server 2016 或 SQL Server 2017 的實例上安裝新的套件, 並提供電腦開啟的埠 80, 而且您具有系統管理員許可權。

> [!IMPORTANT] 
> 請務必將封裝安裝到與目前實例相關聯的預設程式庫。 永遠不要將封裝安裝到使用者目錄。

此程式會使用 Rgui.exe, 但您可以使用 RTerm 或任何其他支援提高存取權的 R 命令列工具。

## <a name="install-a-package-using-rgui"></a>使用 Rgui.exe 安裝套件

1. [判斷實例程式庫的位置](../package-management/r-package-information.md)。 流覽至安裝 R 工具的資料夾。 例如, SQL Server 2017 預設實例的預設路徑如下所示:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. 以滑鼠右鍵按一下 [Rgui.exe], 然後選取 [以**系統管理員身分執行**]。 如果您沒有必要的許可權, 請洽詢資料庫管理員, 並提供您所需的套件清單。

1. 從命令列中, 如果您知道套件名稱, 您可以輸入:`install.packages("the_package-name")`封裝名稱需要雙引號。

1. 當系統要求您提供鏡像網站時, 請選取方便您的位置使用的任何網站。

如果目標封裝相依于其他套件, R 安裝程式會自動下載並為您進行安裝。

如果您有多個 SQL Server 實例, 例如 SQL Server 2016 R 服務和 SQL Server Machine Learning 服務的並存實例, 如果您想要在這兩個內容中使用封裝, 請分別針對每個實例執行安裝。 無法在實例之間共用封裝。

## <a name = "bkmk_offlineInstall"></a>使用 R 工具進行離線安裝

如果伺服器無法存取網際網路, 則需要額外的步驟來準備套件。 若要在無法存取網際網路的伺服器上安裝 R 套件, 您必須:

+ 事先分析相依性。
+ 將目標套件下載到具有網際網路存取的電腦。
+ 將任何必要的套件下載至同一部電腦, 並將所有套件放在單一套件封存中。
+ 如果封存檔案不是壓縮格式, 請將其壓縮。
+ 將封裝封存複製到伺服器上的位置。
+ 安裝指定封存檔案作為來源的目標套件。

> [!IMPORTANT] 
>  開始安裝**之前**, 請務必分析所有相依性並下載**所有**必要的套件。 我們建議您[miniCRAN](https://mran.microsoft.com/package/miniCRAN)此程式。 此 R 套件會接受您想要安裝的套件清單、分析相依性, 並為您取得所有的壓縮檔案。 miniCRAN 接著會建立可複製到伺服器電腦的單一存放庫。 如需詳細資訊, 請參閱[使用 MiniCRAN 建立本機套件存放庫](create-a-local-package-repository-using-minicran.md)

此程式假設您已備妥所需的所有套件 (壓縮格式), 並準備好將它們複製到伺服器。

1. 將封裝壓縮的檔案或多個封裝的完整存放庫 (包含 zip 格式的所有封裝) 複製到伺服器可以存取的位置。

2. 在安裝實例 R 工具的伺服器上開啟資料夾。 例如, 如果您在具有 SQL Server 2016 R 服務的系統上使用 Windows 命令提示字元, 請切換至`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`。

3. 以滑鼠右鍵按一下 Rgui.exe 或 RTerm, 然後選取 [以**系統管理員身分執行**]。

4. 執行 R 命令`install.packages` , 並指定封裝或存放庫名稱, 以及壓縮檔案的位置。

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    此命令會從本機 zip `mynewpackage`壓縮檔案解壓縮 R 封裝, 假設您已將複本儲存在`C:\Temp\Downloaded packages`目錄中, 並將封裝安裝在本機電腦上。 如果封裝有任何相依性, 安裝程式會檢查程式庫中的現有套件。 如果您已建立包含相依性的存放庫, 安裝程式也會安裝必要的套件。

    如果實例程式庫中沒有任何必要的封裝, 而且在壓縮的檔案中找不到, 則安裝目標封裝會失敗。

## <a name="see-also"></a>另請參閱

+ [安裝新的 R 封裝](install-additional-r-packages-on-sql-server.md)
+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)
