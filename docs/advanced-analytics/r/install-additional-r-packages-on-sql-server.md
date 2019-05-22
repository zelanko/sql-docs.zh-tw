---
title: 安裝新的 R 語言套件-SQL Server Machine Learning 服務
description: 將新的 R 套件新增至 SQL Server 2016 R Services 或 SQL Server 2017 Machine Learning 服務 （資料庫）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b8c935400188ae6905a9915907fb097d02100ad2
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994202"
---
# <a name="install-new-r-packages-on-sql-server"></a>SQL Server 上安裝新的 R 套件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何將新的 R 套件安裝至啟用機器學習服務的位置的 SQL Server 的執行個體。 有多種方法來安裝新的 R 套件，視您擁有 SQL server 版本，和伺服器是否有網際網路連線而定。 下列適用於新的套件安裝種可行的。

| 方法                           | Permissions               | 遠端/本機 |
|------------------------------------|---------------------------|--------------|
| [使用傳統的 R 套件管理員](use-r-package-managers-on-sql-server.md)  | 管理 | 本機 |
| [使用 RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  系統管理員啟用資料庫角色之後 | both|
| [使用 T-SQL （建立外部程式庫）](install-r-packages-tsql.md) | 系統管理員啟用資料庫角色之後 | both 

## <a name="who-installs-permissions"></a>誰會安裝 （權限）

R 套件程式庫實際上位於 SQL Server 執行個體，在具有限制存取的安全資料夾中的 [Program Files] 資料夾。 寫入此位置需要系統管理員權限。

非系統管理員可以安裝套件，但這麼做還需要額外的設定和功能在初始安裝中無法使用。 有兩種方法來進行非系統管理員套件安裝：RevoScaleR 使用版本 9.0.1 （英文） 和更新版本，或使用 CREATE EXTERNAL LIBRARY (只有 SQL Server 2017)。 在 SQL Server 2017 **dbo_owner**或另一個具有 CREATE EXTERNAL LIBRARY 權限的使用者可以將 R 套件安裝到目前的資料庫。

R 開發人員習慣建立辦到中央程式庫時，所需的封裝的使用者程式庫。 這種做法是在 SQL Server 資料庫引擎執行個體中執行的 R 程式碼有問題。 SQL Server 無法從外部的程式庫載入封裝，即使該程式庫位於相同的電腦上。 只有從執行個體文件庫的封裝可以用於 SQL Server 中執行的 R 程式碼。

在伺服器上，通常限制檔案系統存取權，而且即使您擁有系統管理員權限和存取伺服器上的使用者文件資料夾時，執行 SQL Server 中的外部指令碼執行階段無法存取安裝預設執行個體外部的任何封裝程式庫。 

## <a name="considerations-for-package-installation"></a>套件安裝的考量

然後再安裝新的套件，請考慮是否適合在 SQL Server 環境中所指定的封裝啟用的功能。 在強化後的 SQL Server 環境中，您可能想要避免下列：

+ 需要網路存取的套件
+ 需要提高權限的檔案系統存取權的套件
+ 封裝用於 web 開發 」 或 「 無益在 SQL Server 內執行其他工作

## <a name="offline-installation-no-internet-access"></a>離線安裝 （沒有網際網路存取）

一般情況下，裝載生產資料庫的伺服器封鎖網際網路連線。 在這類環境中安裝新的 R 或 Python 套件需要您事先準備套件和相依性，並將檔案複製到離線安裝的伺服器上的資料夾。

識別所有相依性變得複雜。 針對 R，我們建議您使用[miniCRAN 建立本機儲存機制](create-a-local-package-repository-using-minicran.md)然後將傳送到隔離的 SQL Server 執行個體的完整定義的存放庫。

或者，您也可以手動執行下列步驟：

1. 找出所有套件相依性。 
2. 請檢查是否在伺服器上已安裝任何必要的套件。 如果安裝套件時，請確認版本正確無誤。
3. 下載封裝和所有相依性到不同的電腦。
4. 伺服器將檔案移至可存取的資料夾。
5. 執行支援的安裝命令或 DDL 陳述式，以將套件安裝到執行個體文件庫。

### <a name="download-the-package-as-a-zipped-file"></a>下載封裝為 zip 壓縮檔案

在沒有網際網路存取的伺服器上安裝，您必須下載離線安裝的 zip 檔案的格式封裝的副本。 **無法將封裝解壓縮。**

例如，下列程序描述現在若要取得正確的版本[FISHalyseR](https://bioconductor.org/packages/release/bioc/html/FISHalyseR.html)封裝，從 Bioconductor，假設電腦有網際網路存取權。

1.  在 [Package Archives] (封裝封存)  清單中找到 **Windows 二進位** 版本。

2.  以滑鼠右鍵按一下的連結。ZIP 檔案，並選取**另存目標**。

3.  瀏覽至本機資料夾壓縮的封裝會儲存，按一下**儲存**。

    此程序會建立套件的本機複本。 

4. 如果您收到下載錯誤，請嘗試不同的鏡像網站。

5. 在下載封裝封存之後，您可以安裝套件，或將壓縮的封裝複製到沒有網際網路存取的伺服器。

> [!TIP]
> 如果不小心，您要安裝的封裝，而不是下載二進位檔，並也會將已下載的 zip 檔案的複本儲存到您的電腦。 若要判斷檔案的位置安裝封裝時，請觀看的狀態訊息。 您可以將該 zip 的檔案複製到沒有網際網路存取的伺服器。
> 
> 不過，當您取得使用此方法的封裝時，相依性不包含。 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>並排顯示安裝獨立 R 或 Python 伺服器

R 和 Python 功能包含多項 Microsoft 產品，全部都可能共存於同一部電腦上。

如果您安裝 SQL Server 2017 Microsoft Machine Learning Server （獨立式） 或 SQL Server 2016 R Server （獨立式），除了 （SQL Server 2017 Machine Learning 服務和 SQL Server 2016 R Services） 的資料庫內分析，您的電腦有不同所有的 R 工具和程式庫的重複項的每個 R 安裝。

會安裝到 R_SERVER 程式庫的套件僅供在獨立伺服器，且無法存取 SQL Server （資料庫內） 執行個體。 一律使用`R_SERVICES`安裝您想要使用 SQL Server 上的資料庫中的封裝時的程式庫。 如需路徑的詳細資訊，請參閱 <<c0> [ 封裝程式庫位置](installing-and-managing-r-packages.md#package-library-location)。


## <a name="see-also"></a>另請參閱

+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)
