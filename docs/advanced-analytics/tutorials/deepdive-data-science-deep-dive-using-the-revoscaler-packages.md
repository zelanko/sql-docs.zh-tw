---
title: RevoScaleR 深入教學課程
description: 在此教學課程系列中，您將了解如何使用 SQL Server 機器學習 R 整合來呼叫 RevoScaleR 函式。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fc1f427659155b5379a681787a633b6037b4bd87
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76918832"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>教學課程：搭配 SQL Server 資料使用 RevoScaleR R 函式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這個多部分的教學課程系列中，會為您介紹與資料科學相關聯工作的一些 **RevoScaleR** 函式。 在此程序中，您將會了解如何建立遠端計算內容、在本機與遠端計算內容之間移動資料，以及在遠端 SQL Server 上執行 R 程式碼。 您也會了解如何在本機與遠端伺服器上分析及繪製資料，以及如何建立及部署模型。

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 是 Microsoft R 套件，可提供資料科學和機器學習工作負載的分散式和平行處理。 針對 SQL Server 中的 R 開發，**RevoScaleR** 是其中一個核心內建套件，包含用來建立資料來源物件、設定計算內容、管理套件的功能，以及最重要的功能：從匯入到視覺效果和分析，端對端使用資料。 SQL Server 中的機器學習演算法相依於 **RevoScaleR** 資料來源。 基於 **RevoScaleR** 的重要性，知道何時以及如何呼叫其函式是必要的技能。 

## <a name="prerequisites"></a>Prerequisites

+ 使用 R 功能的 [SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)，或 [SQL Server R 服務 (資料庫內)](../install/sql-r-services-windows-install.md)
  
+ [資料庫權限](../security/user-permission.md) 和 SQL Server 資料庫使用者登入

+ [Transact-SQL](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ IDE，例如 RStudio 或 R 包含內建 RGUI.EXE 工具

若要在本機與遠端計算內容之間來回切換，您需要兩個系統。 本機通常是具有足夠資料科學工作負載能力的開發工作站。 在此情況下，遠端會是已啟用 R 功能的 SQL Server。 

切換計算內容的前提是在本機和遠端系統上具有相同版本的 **RevoScaleR**。 在本機工作站上，您可以藉由安裝 Microsoft R Client 來取得 **RevoScaleR** 套件和相關提供者。

如果您需要將用戶端和伺服器放在同一部電腦上，請務必安裝第二組 Microsoft R 程式庫，以便從「遠端」用戶端傳送 R 指令碼。 請勿使用在 SQL Server 執行個體的程式檔案中安裝的 R 程式庫。 尤其是，如果您使用一台電腦，則在這兩個位置都需要 **RevoScaleR** 程式庫，以便支援用戶端和伺服器作業。

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

如需用戶端設定的指示，請參閱[設定 R 開發的資料科學用戶端](../r/set-up-a-data-science-client.md)。


## <a name="r-development-tools"></a>R 開發工具

R 開發人員通常會使用 IDE 來撰寫 R 程式碼以及進行偵錯。 以下是一些建議：

- **Visual Studio R 工具** (RTVS) 是免費的外掛程式，可提供 Intellisense、偵錯及 Microsoft R 的支援。您可以將它用於 R 伺服器和 SQL Server Machine Learning 服務。 若要下載，請參閱 [適用於 Visual Studio 的 R 工具](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019)。

- **RStudio** 是其中一個比較常見的 R 開發環境。 如需詳細資訊，請參閱 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)。

- 當您在 SQL Server 或 R 用戶端中安裝 R 時，預設也會安裝基本 R 工具 (R.exe、RTerm.exe、RScripts.exe)。 如果您不想要安裝 IDE，可以使用內建的 R 工具來執行本教學課程中的程式碼。

回想一下，本機和遠端電腦上都需要 **RevoScaleR**。 您無法使用 RStudio 的一般安裝或遺漏 Microsoft R 程式庫的其他環境來完成本教學課程。 如需詳細資訊，請參閱 [Set Up a Data Science Client](../r/set-up-a-data-science-client.md)(設定資料科學用戶端)。

## <a name="summary-of-tasks"></a>工作摘要

+ 資料最初是從 CSV 檔案或 XDF 檔案取得。 您使用 **RevoScaleR** 套件中的函式，將資料匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。
+ 模型定型和評分將會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 計算內容來執行。 
+ 使用 **RevoScaleR** 函式來建立新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，以儲存您的評分結果。
+ 在伺服器與本機計算內容中建立繪圖。
+ 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫 (在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中執行 R) 中的資料定型模型。
+ 擷取資料子集，並將它儲存為 XDF 檔案，以便在本機工作站上重複用於分析。
+ 藉由開啟與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的 ODBC 連線，取得要評分的新資料。 評分是在本機工作站上完成。
+ 建立自訂 R 函式，並且在伺服器計算內容中執行，以執行模擬。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [教學課程 1：建立資料庫與權限](deepdive-work-with-sql-server-data-using-r.md)