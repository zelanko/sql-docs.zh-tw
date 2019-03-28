---
title: RevoScaleR 函式的深入教學課程-SQL Server Machine Learning
description: 在本教學課程，了解如何使用 SQL Server Machine Learning R 整合的 RevoScaleR 函式的呼叫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 48d65bfe54890c5ea0d8bfdca9c76fa0978a917d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511725"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>教學課程：使用 RevoScaleR R 函式與 SQL Server 資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)是提供分散式的 Microsoft R 封裝和平行處理的資料科學與機器學習服務工作負載。 適用於 SQL Server 中的 R 開發**RevoScaleR**是核心的其中一個內建的套件，與函式來建立資料來源物件，設定計算內容，管理封裝，最重要的是： 使用資料端對端，從 視覺效果和分析資料的匯入。 SQL Server 中的機器學習服務演算法有相依性**RevoScaleR**資料來源。 指定的重要性**RevoScaleR**、 了解的時機，以及如何呼叫其函式是最基本的技巧。 

您會在此多部分的教學課程中，引進了一組**RevoScaleR**相關聯的資料科學工作的函式。 在過程中，您將了解如何建立遠端計算內容中，本機和遠端計算內容之間移動資料，並在遠端 SQL Server 上執行 R 程式碼。 您也了解如何分析並繪製資料在本機和遠端伺服器，以及如何建立和部署模型。

## <a name="prerequisites"></a>先決條件

+ [SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)與 [R] 功能，或[SQL Server 2016 R Services （資料庫）](../install/sql-r-services-windows-install.md)
  
+ [資料庫權限](../security/user-permission.md)和 SQL Server 資料庫使用者登入

+ [Transact-SQL](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ IDE，例如 RStudio 或內建的 RGUI 工具隨附於 R

本機和遠端計算內容之間來回切換，您需要兩個系統。 本機通常是使用足夠的能力，用於資料科學工作負載的開發工作站。 遠端在此情況下是 SQL Server 2017 或 SQL Server 2016 已啟用 R 功能。 

切換計算內容基於相同版本**RevoScaleR**本機和遠端系統上。 您可以在本機工作站上，取得**RevoScaleR**封裝和相關的提供者，藉由安裝 Microsoft R Client。

如果您需要將用戶端和伺服器放在同一部電腦上，請務必安裝適用於從 「 遠端 」 的用戶端傳送 R 指令碼的 Microsoft R 程式庫的第二組。 請勿使用安裝程式檔案的 SQL Server 執行個體中的 R 程式庫。 具體而言，如果您使用一部電腦，您需要**RevoScaleR**文件庫中的這些位置，以支援用戶端和伺服器作業。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

如需用戶端組態的指示，請參閱 <<c0> [ 設定適用於 R 開發的資料科學用戶端](../r/set-up-a-data-science-client.md)。


## <a name="r-development-tools"></a>R 開發工具

R 開發人員通常會使用 Ide 來撰寫和偵錯的 R 程式碼。 以下是一些建議：

- **適用於 Visual Studio R 工具**(RTVS) 是免費的外掛程式提供 Intellisense、 偵錯，以及支援 Microsoft。您可以使用 R Server 和 SQL Server Machine Learning 服務來使用它。 若要下載，請參閱 [適用於 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)。

- **RStudio** 是其中一個比較常見的 R 開發環境。 如需詳細資訊，請參閱 < [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/)。

- 當您安裝 R 在 SQL Server 或 R 用戶端時，預設也會安裝基本的 R 工具 (R.exe、 RTerm.exe、 RScripts.exe)。 如果您不想安裝 IDE，您可以使用內建的 R 工具來執行本教學課程中的程式碼。

請記得， **RevoScaleR**本機和遠端電腦上需要。 您無法完成此教學課程使用一般安裝的 RStudio 或其他遺失的 Microsoft R 程式庫的環境。 如需詳細資訊，請參閱 [Set Up a Data Science Client](../r/set-up-a-data-science-client.md)(設定資料科學用戶端)。

## <a name="summary-of-tasks"></a>工作的摘要

+ 資料最初是從 CSV 檔案或 XDF 檔案取得。 資料匯入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用中的函式**RevoScaleR**封裝。
+ 模型定型和計分則使用執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]計算內容。 
+ 使用**RevoScaleR**來建立新的函式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表來儲存您的計分結果。
+ 在伺服器上建立兩個繪圖，並在本機計算內容。
+ 根據中的資料來定型模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中執行 R 的資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。
+ 擷取資料的子集，並將它儲存為 XDF 檔案，以便在分析中重複使用本機工作站上。
+ 取得新的資料進行評分，藉由開啟的 ODBC 連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 計分是在本機工作站上完成。
+ 建立自訂的 R 函數並執行伺服器中計算內容，以執行模擬。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [第 1 課：建立資料庫和權限](deepdive-work-with-sql-server-data-using-r.md)