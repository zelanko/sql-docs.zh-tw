---
title: 安裝新的 R 語言套件
description: 將新的 R 封裝新增至 SQL Server 2016 R Services 或 SQL Server 2017 Machine Learning Services (資料庫內)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1a6459d45d36ff69bdafb62a712e18937bf8eb30
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470106"
---
# <a name="install-new-r-packages-on-sql-server"></a>在 SQL Server 上安裝新的 R 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何將新的 R 封裝安裝到啟用機器學習服務的 SQL Server 實例。 有多種方法可以安裝新的 R 封裝, 視您擁有的 SQL Server 版本以及伺服器是否有網際網路連線而定。 下列是可能的新封裝安裝方法。

| 方法                           | Permissions               | 遠端/本機 |
|------------------------------------|---------------------------|--------------|
| [使用傳統 R 套件管理員](use-r-package-managers-on-sql-server.md)  | 管理 | 本機 |
| [使用 RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  之後的資料庫角色已啟用系統管理員 | both|
| [使用 T-sql (建立外部程式庫)](install-r-packages-tsql.md) | 之後的資料庫角色已啟用系統管理員 | both 

## <a name="who-installs-permissions"></a>安裝者 (許可權)

R 封裝程式庫實際上位於 SQL Server 實例的 Program Files 資料夾中, 位於具有限制存取的安全資料夾中。 寫入此位置需要系統管理員許可權。

非系統管理員可以安裝套件, 但這麼做需要在初始安裝中無法使用其他設定和功能。 非系統管理員套件安裝有兩種方法:使用9.0.1 和更新版本的 RevoScaleR, 或使用 [建立外部程式庫] (僅限 SQL Server 2017)。 在 SQL Server 2017 中, **dbo_owner**或具有 CREATE EXTERNAL LIBRARY 許可權的另一位使用者可以將 R 封裝安裝到目前的資料庫。

如果集中存放的程式庫已關閉限制, 則 R 開發人員習慣建立所需套件的使用者程式庫。 這種做法對於在 SQL Server 資料庫引擎實例中執行的 R 程式碼而言, 會造成問題。 SQL Server 無法從外部程式庫載入封裝, 即使該程式庫位於相同的電腦上也一樣。 只有來自實例程式庫的封裝可以在 SQL Server 中執行的 R 程式碼中使用。

伺服器上的檔案系統存取通常會受到限制, 即使您擁有伺服器上的使用者檔資料夾的管理員許可權和存取權, 在 SQL Server 中執行的外部腳本執行時間還是無法存取安裝在預設實例外部的任何套件機庫. 

## <a name="considerations-for-package-installation"></a>套件安裝的考慮

安裝新套件之前, 請考慮指定封裝所啟用的功能是否適用于 SQL Server 環境。 在強化的 SQL Server 環境中, 您可能會想要避免下列情況:

+ 需要網路存取的套件
+ 需要提升檔案系統存取權的封裝
+ 封裝用於 網頁程式開發或其他無法透過在 SQL Server 內執行的工作

## <a name="offline-installation-no-internet-access"></a>離線安裝 (無法存取網際網路)

一般來說, 裝載生產資料庫的伺服器會封鎖網際網路連線。 若要在這類環境中安裝新的 R 或 Python 套件, 您必須事先準備封裝和相依性, 然後將檔案複製到伺服器上的資料夾以進行離線安裝。

識別所有相依性會變得複雜。 針對 R, 建議您使用[miniCRAN 來建立本機儲存](create-a-local-package-repository-using-minicran.md)機制, 然後將完整定義的存放庫傳輸至隔離的 SQL Server 實例。

或者, 您也可以手動執行下列步驟:

1. 識別所有套件相依性。 
2. 檢查伺服器上是否已安裝任何必要的套件。 如果已安裝封裝, 請確認版本是否正確。
3. 將套件和所有相依性下載至另一部電腦。
4. 將檔案移至伺服器可存取的資料夾。
5. 執行支援的安裝命令或 DDL 語句, 以將封裝安裝至實例程式庫。

### <a name="download-the-package-as-a-zipped-file"></a>將套件下載為壓縮檔案

若要在沒有網際網路存取的伺服器上安裝, 您必須以壓縮檔案的格式下載封裝的複本, 以進行離線安裝。 **請勿將封裝解壓縮。**

例如, 下列程式說明從 Bioconductor 取得正確版本的[FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html)套件, 假設電腦可以存取網際網路。

1.  在 [Package Archives] (封裝封存)  清單中找到 **Windows 二進位** 版本。

2.  以滑鼠右鍵按一下的連結。ZIP 檔案, 然後選取 [**另存目標**]。

3.  流覽至儲存壓縮封裝的本機資料夾, 然後按一下 [儲存]。

    此程序會建立套件的本機複本。 

4. 如果您收到下載錯誤, 請嘗試其他鏡像網站。

5. 下載封裝封存之後, 您可以安裝套件, 或將壓縮的封裝複製到無法存取網際網路的伺服器。

> [!TIP]
> 如果您誤安裝封裝, 而不是下載二進位檔, 下載的壓縮檔案複本也會儲存到您的電腦上。 在安裝套件時監看狀態訊息, 以判斷檔案位置。 您可以將該壓縮檔案複製到無法存取網際網路的伺服器。
> 
> 不過, 當您使用此方法取得封裝時, 不會包含相依性。 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>與獨立 R 或 Python 伺服器並存安裝

R 和 Python 功能包含在數個 Microsoft 產品中, 它們全都可以並存于同一部電腦上。

如果您已安裝 SQL Server 2017 Microsoft Machine Learning Server (獨立式) 或 SQL Server 2016 R Server (獨立式), 除了資料庫內分析 (SQL Server 2017 Machine Learning Services 和 SQL Server 2016 R Services) 之外, 您的電腦也會有不同的適用于每個的 R 安裝, 其中包含所有 R 工具和程式庫的重複專案。

安裝到 R_SERVER 程式庫的套件僅供獨立伺服器使用, 而且不能由 SQL Server (資料庫內) 實例存取。 安裝您想`R_SERVICES`要在 SQL Server 的資料庫中使用的套件時, 請一律使用程式庫。 如需路徑的詳細資訊, 請參閱[套件程式庫位置](../package-management/default-packages.md)。

## <a name="see-also"></a>另請參閱

+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)
