---
title: 教學課程，需 RevoScaleR 函式與 SQL Server Machine Learning |Microsoft Docs
description: 在本教學課程，了解如何呼叫 RevoScaleR 函式以支援 R 的 SQL Server Machine Learning 中已啟用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ee810c998f8aecf17c3496540c65471e0b29e102
ms.sourcegitcommit: a083e9d59e2014a06cda9138b7e17c17ecab90e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/11/2018
ms.locfileid: "44343083"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>SQL Server 資料的教學課程： 使用 RevoScaleR R 函式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 是提供分散式和平行處理的資料科學與機器學習服務工作負載的 Microsoft R 套件。 SQL Server 中的 R 開發，RevoScaleR 是其中一個核心內建套件，但與函式來設定計算內容，管理封裝，最重要的是： 使用資料端對端，從 視覺效果和分析資料的匯入。 SQL Server 中的機器學習演算法會對 RevoScaleR 資料來源中的相依性。 提供的 RevoScaleR 的重要性，了解何時以及如何呼叫其函式是最基本的技巧。 

在本教學課程中，您將了解如何建立遠端計算內容中，本機和遠端計算內容之間移動資料，並在遠端 SQL Server 上執行 R 程式碼。 您也了解如何分析並繪製資料在本機和遠端伺服器，以及如何建立和部署模型。

+ 資料最初是從 CSV 檔案或 XDF 檔案取得。 資料匯入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]RevoScaleR 封裝中使用函式。
+ 模型定型和計分則使用執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]計算內容。 
+ 使用 RevoScaleR 函式來建立新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表來儲存您的計分結果。
+ 在伺服器上建立兩個繪圖，並在本機計算內容。
+ 根據中的資料來定型模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中執行 R 的資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。
+ 擷取資料的子集，並將它儲存為 XDF 檔案，以便在分析中重複使用本機工作站上。
+ 取得新的資料進行評分，藉由開啟的 ODBC 連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 計分是在本機工作站上完成。
+ 建立自訂的 R 函數並執行伺服器中計算內容，以執行模擬。

## <a name="target-audience"></a>目標對象

本教學課程適合資料科學家或人員已稍微熟悉 R，以及資料科學工作，例如摘要和模型建立。 不過，提供所有程式碼，因此即使您不熟悉 R，您可以執行程式碼，並跟著做，請假設您有必要的伺服器和用戶端環境。

您也應該熟悉[!INCLUDE[tsql](../../includes/tsql-md.md)]語法並知道如何存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫使用這類的工具：

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Visual Studio 中的資料庫工具 
+ 免費[適用於 Visual Studio Code 的 mssql 擴充功能](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)。
  
> [!TIP]
> 在每堂課之間儲存 R 工作區，以輕鬆地從先前離開的地方繼續進行。

## <a name="prerequisites"></a>先決條件

- **支援 R 的 SQL Server**
  
    安裝[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)R 功能，或安裝[SQL Server 2016 R Services （資料庫）](../install/sql-r-services-windows-install.md)。

    請確定已啟用外部指令碼、 Launchpad 服務正在執行，而且您有權限來存取服務。
  
-  **資料庫權限**
  
    若要執行用來定型模型的查詢，您必須具有資料儲存所在資料庫的 **db_datareader** 權限。 若要執行 R，您的使用者必須具有的權限 EXECUTE ANY EXTERNAL SCRIPT。

-   **資料科學開發電腦**
  
    本機和遠端計算內容之間來回切換，您需要兩個系統。 本機通常是使用足夠的能力，用於資料科學工作負載的開發工作站。 遠端在此情況下是 SQL Server 2017 或 SQL Server 2016 已啟用 R 功能。 
    
    於本機和遠端系統上具有相同版本 RevoScaleR 中預測有切換計算內容。 在本機工作站上，您可以取得 RevoScaleR 套件及相關的提供者安裝或使用下列任何一個：[在 Azure 上的資料科學 VM](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)， [（免費） 的 Microsoft R Client](https://docs.microsoft.com/en-us/machine-learning-server/r-client/what-is-microsoft-r-client)，或[Microsoft Machine Learning Server （獨立式）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-install)。 安裝獨立伺服器 選項中，使用 Linux 或 Windows 安裝程式的免費開發人員版本。 您也可以使用 SQL Server 安裝程式安裝在獨立伺服器。
      
-   **其他 R 套件**
  
    在本教學課程中，您會安裝下列封裝： **dplyr**， **ggplot2**， **ggthemes**， **reshape2**，和**e1071**. 相關指示會隨本教學課程一起提供。
  
    所有套件必須都安裝在兩個地方： 用來開發 R 解決方案，在工作站上及執行 R 指令碼所在的 SQL Server 電腦上。 如果您沒有在伺服器電腦上安裝封裝的權限，請要求系統管理員。 
    
    **請不要將套件安裝至使用者程式庫。** 套件必須安裝在 SQL Server 執行個體使用的 R 套件程式庫。

## <a name="r-development-tools"></a>R 開發工具

R 開發人員通常會使用 Ide 來撰寫和偵錯的 R 程式碼。 以下是一些建議：

- **適用於 Visual Studio R 工具**(RTVS) 是免費的外掛程式提供 Intellisense、 偵錯，以及支援 Microsoft。您可以使用 R Server 和 SQL Server Machine Learning 服務來使用它。 若要下載，請參閱 [適用於 Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)。

- **RStudio** 是其中一個比較常見的 R 開發環境。 如需詳細資訊，請參閱 < [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/)。

- 當您安裝 R 在 SQL Server 或 R 用戶端時，預設也會安裝基本的 R 工具 (R.exe、 RTerm.exe、 RScripts.exe)。 如果您不想安裝 IDE，您可以使用內建的 R 工具來執行本教學課程中的程式碼。

RevoScaleR，需要在本機和遠端電腦上的重新叫用。 您無法完成此教學課程使用一般安裝的 RStudio 或其他遺失的 Microsoft R 程式庫的環境。 如需詳細資訊，請參閱 [Set Up a Data Science Client](../r/set-up-a-data-science-client.md)(設定資料科學用戶端)。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [第 1 課： 建立資料庫和權限](deepdive-work-with-sql-server-data-using-r.md)

