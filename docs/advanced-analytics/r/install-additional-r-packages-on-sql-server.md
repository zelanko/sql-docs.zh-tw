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
ms.openlocfilehash: e05842a8e8a5a1d2454dbbe500b4d5aa95fca660
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707076"
---
# <a name="install-new-r-packages-on-sql-server"></a>SQL Server 上安裝新的 R 封裝
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何安裝新的 R 封裝在已啟用機器學習的 SQL Server 執行個體。 有多種方法，如安裝新的 R 封裝，根據您擁有 SQL server 版本，以及伺服器是否有網際網路連線。 適用於新的封裝安裝下列方法也有可能的。

| 方法                           | Permissions               | 遠端/本機 |
|------------------------------------|---------------------------|--------------|
| [使用傳統的 R 封裝管理員](use-r-package-managers-on-sql-server.md)  | 管理 | 本機 |
| [使用 RevoScaleR](use-revoscaler-to-manage-r-packages.md) |  系統管理員啟用資料庫角色之後 | both|
| [使用 T-SQL （建立外部程式庫）](install-r-packages-tsql.md) | 系統管理員啟用資料庫角色之後 | both 

## <a name="who-installs-permissions"></a>誰會安裝 （權限）

R 封裝程式庫實際位於您 SQL Server 執行個體，且限制存取安全的資料夾中的 Program Files 資料夾中。 寫入此位置需要系統管理員權限。

非系統管理員可以安裝封裝，但這樣做需要 addititional 組態和功能在初始安裝中無法使用。 有兩種方法為非系統管理員封裝安裝： RevoScaleR 使用 9.0.1 版本和更新版本，或使用建立外部程式庫 (只有 SQL Server 2017)。 在 SQL Server 2017， **dbo_owner**或建立外部程式庫的權限的其他使用者可以將 R 封裝安裝到目前的資料庫。

R 開發人員都習慣建立 off-limits 中央程式庫時，所需封裝的使用者程式庫。 這種作法是在 SQL Server 資料庫引擎執行個體中執行的 R 程式碼有問題。 SQL Server 無法從外部程式庫，載入封裝，即使該程式庫是在相同電腦上。 只有從執行個體文件庫的封裝可以用於 SQL Server 中執行的 R 程式碼。

通常限制檔案系統存取的伺服器上，而且即使您擁有系統管理員權限及存取伺服器上的使用者文件資料夾時，執行 SQL Server 中的外部指令碼執行階段無法存取安裝預設執行個體外部的任何封裝程式庫。 

## <a name="considerations-for-package-installation"></a>封裝安裝的考量

然後再安裝新的封裝，請考慮指定封裝所啟用的功能是否適合使用 SQL Server 環境。 在強行寫入 SQL Server 環境中，您可能想要避免下列：

+ 需要網路存取的封裝
+ 需要 Java 或不常使用的 SQL Server 環境中的其他架構封裝
+ 需要提高權限的檔案系統存取的封裝
+ 封裝會用於 web 程式開發或其他不在 SQL Server 內執行獲益的工作

## <a name="offline-installation-no-internet-access"></a>離線安裝 （無網際網路存取）

一般情況下，裝載生產資料庫的伺服器封鎖網際網路連線。 在這類環境中安裝新的 R 或 Python 封裝需要您事先準備封裝和相依性，並將檔案複製到離線安裝的伺服器上的資料夾。

識別所有相依性變複雜。 ，我們建議您使用[建立本機儲存機制 miniCRAN](create-a-local-package-repository-using-minicran.md) ，然後再傳輸到隔離的 SQL Server 執行個體的完整定義的儲存機制。

Alternativley，您可以執行此步驟以手動方式：

1. 找出所有套件相依性。 
2. 請檢查任何必要的封裝是否已安裝在伺服器上。 如果已安裝此套件，請確認版本是否正確。
3. 下載封裝和所有相依性到另一部電腦。
4. 檔案伺服器移至可存取的資料夾。
5. 執行支援的安裝命令或 DDL 陳述式，將封裝安裝到執行個體文件庫。

### <a name="download-the-package-as-a-zipped-file"></a>下載為 zip 檔案的套件

在沒有網際網路存取的伺服器上安裝，您必須下載離線安裝的 zip 檔案格式的封裝副本。 **無法將封裝解壓縮。**

例如，下列程序描述現在以取得正確的版本[FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html)封裝，從 Bioconductor，假設電腦有網際網路存取權。

1.  在 [Package Archives] (封裝封存)  清單中找到 **Windows 二進位** 版本。

2.  以滑鼠右鍵按一下連結。ZIP 檔案，並選取**另存目標**。

3.  瀏覽至本機資料夾壓縮的封裝會儲存位置，而按一下**儲存**。

    此程序會建立套件的本機複本。 

4. 如果您收到的下載錯誤，請嘗試不同的鏡像網站。

5. 已下載封裝封存之後，您可以安裝封裝，或將壓縮的封裝複製到沒有網際網路存取的伺服器。

> [!TIP]
> 如果不小心安裝而不是下載二進位檔案的套件，下載 zip 檔案的副本也會儲存到您的電腦。 查看已安裝此套件，來判斷檔案位置的狀態訊息。 您可以將該 zip 的檔案複製到沒有網際網路存取的伺服器。
> 
> 不過，當您取得使用此方法的封裝時，相依性不包含。 


## <a name="side-by-side-installation-with-standalone-r-or-python-servers"></a>與獨立 R 或 Python 伺服器-並存安裝

許多 Microsoft 產品，全部都是無法共存於同一部電腦上包含 R，並將 Python 的功能。

如果您安裝 SQL Server 2017 Microsoft Machine Learning 伺服器 （獨立） 或 SQL Server 2016 R 伺服器 （獨立） 除了 （SQL Server 2017 機器學習服務和 SQL Server 2016 R Services） 的資料庫分析時，您的電腦有不同針對每個重複項目，所有的 R 工具和程式庫的 R 安裝。

封裝安裝至 R_SERVER 文件庫只由獨立伺服器，並無法存取 SQL Server （資料庫） 執行個體。 一律使用`R_SERVICES`安裝您想要使用 SQL Server 上的資料庫中的封裝時，程式庫。 如需路徑的詳細資訊，請參閱[封裝程式庫位置](installing-and-managing-r-packages.md#package-library-location)。


## <a name="see-also"></a>另請參閱

+ [安裝新的 Python 封裝](../python/install-additional-python-packages-on-sql-server.md)
+ [教學課程、範例、解決方案](../tutorials/machine-learning-services-tutorials.md)