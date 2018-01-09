---
title: "資料科學深入探討： 搭配 SQL Server 使用 RevoScaleR 封裝 |Microsoft 文件"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: a8fe18a578391beaae79259440779b0a76336ee2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="data-science-deep-dive-using-the-revoscaler-packages-with-sql-server"></a>資料科學深入探討： 搭配 SQL Server 使用 RevoScaleR 封裝

本教學課程示範如何使用增強的 R 封裝中提供[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]使用 SQL Server 資料，並建立可調整的 R 解決方案，做為運算環境中使用的伺服器，進行高效能巨量資料分析。

您了解如何建立遠端計算內容中，本機和遠端計算內容之間移動資料，以及遠端的 SQL Server 上執行 R 程式碼。 此外，您也會學習如何分析和繪製的資料，包括本機或遠端伺服器，以及如何建立及部署模型。

> [!NOTE]
> 
> 本教學課程會在 Windows 中，才能存取 SQL Server 資料，並使用資料庫中的計算內容。 如果您想要在其他內容，例如 Teradata、 Linux 或是 Hadoop，使用 R，請參閱這些 Microsoft R Server 教學課程： 
> + [使用 R 伺服器，而 sparklyr](https://docs.microsoft.com/machine-learning-server/r/tutorial-sparklyr-revoscaler)
> + [在 25 個函數中探索 R 和 ScaleR (英文)](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)
> + [在 Hadoop MapReduce ScaleR 快速入門](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-hadoop)

## <a name="overview"></a>概觀

您移動資料和交換計算內容經常遇到彈性和處理的強大的 RevoScaleR 封裝，在本教學課程。 為了說明，以下是一些工作在本教學課程：

+ 資料最初是從 CSV 檔案或 XDF 檔案取得。 資料匯入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 RevoScaleR 封裝中的函式。
+ 模型的定型和計分使用執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]計算內容。 
+ 使用 RevoScaleR 函數來建立新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表來儲存計分結果。
+ 在伺服器上建立兩個繪圖，並在本機計算內容。
+ 定型模型中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中執行 R 的資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。
+ 擷取資料的子集，並將它儲存為您的本機工作站上的重新分析中使用 XDF 檔案。
+ 取得新的資料進行評分，藉由開啟的 ODBC 連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 計分是在本機工作站上完成。
+ 建立自訂的 R 函數並執行伺服器中計算內容執行模擬。

### <a name="article-list-and-time-required"></a>發行項清單以及所需時間

本教學課程需要大約 75 分鐘才能完成，不包括安裝程式。

1. [使用 SQL Server 資料使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [使用 RxSqlServerData 建立 SQL Server 資料物件](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [查詢及修改 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [定義及使用計算內容](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [建立和執行 R 指令碼](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [使用 R 的 SQL Server 資料視覺化](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [建立 R 模型](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [分數新的資料](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [使用 R 轉換資料](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [將資料載入至使用 rxImport 記憶體](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [建立新的 SQL Server 資料表使用 rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [使用 rxDataStep 執行區塊處理分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [分析本機計算內容中的資料](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [將資料從 SQL Server 使用 XDF 檔案移動](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [建立簡單的模擬](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>目標對象

本教學課程僅適用於資料科學家或已經是有些熟悉 R、 與資料科學工作，例如摘要和模型的建立。  不過，所有的程式碼，所以即使您是新手 R，您可以執行的程式碼，並跟著做，請假設您擁有所需的伺服器和用戶端環境。

您也應該熟悉[!INCLUDE[tsql](../../includes/tsql-md.md)]語法並知道如何存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫使用這類工具：

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Visual Studio 中的資料庫工具 
+ 免費[mssql 擴充 Visual Studio 程式碼](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)。
  
> [!TIP]
> 在每堂課之間儲存 R 工作區，以輕鬆地從先前離開的地方繼續進行。

### <a name="prerequisites"></a>Prerequisites

- **支援 R 與 SQL Server**
  
    安裝 SQL Server 2016 並啟用 R 服務 （資料庫）。 或者，安裝 SQL Server 2017，啟用機器學習服務並選擇的 R 語言。
  
-  **資料庫權限**
  
    若要執行用來定型模型的查詢，您必須具有資料儲存所在資料庫的 **db_datareader** 權限。 若要執行 R，您的使用者必須具有權限，EXECUTE ANY EXTERNAL SCRIPT。

-   **資料科學開發電腦**
  
    您必須做的 R 開發環境的電腦上安裝的 RevoScaleR 封裝和相關的提供者。 若要這樣做最簡單的方式是安裝 Microsoft R 用戶端，Microsoft R Server （獨立） 或機器學習伺服器 （獨立）。 
      
    > [!NOTE] 
    > 不支援 Revolution R Enterprise 或 Revolution R Open 的其他版本。
    > 
    > R 的開放原始碼散發不能在此教學課程中，因為只有 RevoScaleR 函式可以使用遠端計算內容。
  
-   **其他 R 套件**
  
    在此教學課程中，您會安裝下列封裝： **dplyr**， **ggplot2**， **ggthemes**， **reshape2**，和**e1071**. 相關指示會隨本教學課程一起提供。
  
    必須安裝所有封裝，在兩個地方： R 指令碼會執行所在的 SQL Server 電腦和您用於開發 R 解決方案，在電腦上。 如果您沒有在伺服器電腦上安裝封裝的權限，請要求系統管理員。 
    
    **請不要將套件安裝至使用者程式庫。** 封裝必須安裝在 SQL Server 執行個體使用的 R 封裝文件庫中。

如需詳細資訊，請參閱[資料科學逐步解說的必要條件](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)。

## <a name="next-step"></a>下一步

[使用 SQL Server 資料使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

