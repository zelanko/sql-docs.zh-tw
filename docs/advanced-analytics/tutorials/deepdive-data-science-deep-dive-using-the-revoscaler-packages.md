---
title: RevoScaleR 函數深入教學課程-SQL Server Machine Learning
description: 在本教學課程中, 您將瞭解如何使用 SQL Server Machine Learning R 整合來呼叫 RevoScaleR 函式。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c326d51e9b3ac4edac61f97bf5f7fa3143d8d350
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470625"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>教學課程：搭配 SQL Server 資料使用 RevoScaleR R 函數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)是 Microsoft R 套件, 可提供資料科學和機器學習工作負載的分散式和平行處理。 針對 SQL Server 中的 R 開發, **RevoScaleR**是其中一個核心內建套件, 其中包含用來建立資料來源物件、設定計算內容、管理封裝, 以及最重要的功能: 從匯入至的端對端處理資料視覺效果和分析。 SQL Server 中的 Machine Learning 演算法相依于**RevoScaleR**的資料來源。 考慮到**RevoScaleR**的重要性, 知道何時以及如何呼叫其函式是一項重要的技巧。 

在這個多部分的教學課程中, 您會針對與資料科學相關聯的工作, 引進一系列的**RevoScaleR**函數。 在此過程中, 您將瞭解如何建立遠端計算內容、在本機和遠端計算內容之間移動資料, 以及在遠端 SQL Server 上執行 R 程式碼。 您也將學習如何在本機和遠端伺服器上分析和繪製資料, 以及如何建立和部署模型。

## <a name="prerequisites"></a>必要條件

+ 使用 R 功能[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md), 或[SQL Server 2016 R Services (資料庫內)](../install/sql-r-services-windows-install.md)
  
+ [資料庫許可權](../security/user-permission.md)和 SQL Server 資料庫使用者登入

+ [Transact-SQL](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ 包含在 R 中的 IDE, 例如 RStudio 或內建的 RGUI.EXE 工具

若要在本機和遠端計算內容之間來回切換, 您需要兩個系統。 本機通常是具有資料科學工作負載足夠能力的開發工作站。 在此情況下, 遠端 SQL Server 2017 或已啟用 R 功能的 SQL Server 2016。 

切換計算內容的前提是在本機和遠端系統上都有相同版本的**RevoScaleR** 。 在本機工作站上, 您可以藉由安裝 Microsoft R Client 來取得**RevoScaleR**封裝和相關的提供者。

如果您需要將用戶端和伺服器放在同一部電腦上, 請務必安裝第二組 Microsoft R 程式庫, 以便從「遠端」用戶端傳送 R 腳本。 請勿使用安裝在 SQL Server 實例之程式檔案中的 R 程式庫。 具體而言, 如果您使用一部電腦, 則在這兩個位置都需要**RevoScaleR**程式庫, 以支援用戶端和伺服器作業。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

如需用戶端設定的指示, 請參閱[設定 R 開發的資料科學用戶端](../r/set-up-a-data-science-client.md)。


## <a name="r-development-tools"></a>R 開發工具

R 開發人員通常會使用 Ide 來撰寫和調試 R 程式碼。 以下是一些建議：

- **Visual Studio R 工具**(RTVS) 是免費的外掛程式, 可提供 Intellisense、偵錯工具和 Microsoft R 的支援。您可以將它用於 R 伺服器和 SQL Server Machine Learning 服務。 若要下載，請參閱 [適用於 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)。

- **RStudio** 是其中一個比較常見的 R 開發環境。 如需詳細資訊, [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)請參閱。

- 當您在 SQL Server 或 R 用戶端中安裝 R 時, 預設也會安裝基本 R 工具 (R .exe、RTerm .exe、Rscripts.exe)。 如果您不想要安裝 IDE, 可以使用內建的 R 工具來執行本教學課程中的程式碼。

回想一下, 本機和遠端電腦上都需要**RevoScaleR** 。 您無法使用 RStudio 的一般安裝或缺少 Microsoft R 程式庫的其他環境來完成本教學課程。 如需詳細資訊，請參閱 [Set Up a Data Science Client](../r/set-up-a-data-science-client.md)(設定資料科學用戶端)。

## <a name="summary-of-tasks"></a>工作摘要

+ 資料最初是從 CSV 檔案或 XDF 檔案取得。 您可以使用**RevoScaleR**套件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的函式將資料匯入至。
+ 模型定型和計分會使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]計算內容來執行。 
+ 使用**RevoScaleR**函數來建立新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料表, 以儲存您的評分結果。
+ 在伺服器和本機計算內容中建立繪圖。
+ 針對在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例中執行 R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料庫中的資料定型模型。
+ 將資料子集解壓縮, 並將它儲存為 XDF 檔案, 以便在本機工作站上重複流量分析。
+ 藉由開啟[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫的 ODBC 連接, 取得要計分的新資料。 評分是在本機工作站上完成。
+ 建立自訂的 R 函式, 並在伺服器計算內容中執行, 以進行模擬。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [第 1 課：建立資料庫和許可權](deepdive-work-with-sql-server-data-using-r.md)