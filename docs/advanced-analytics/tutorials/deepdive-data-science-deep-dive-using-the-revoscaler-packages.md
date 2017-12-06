---
title: "資料科學深入探討︰使用 RevoScaleR 套件 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: dcd06bcdf2fbfbb4aaa405c77429c4bd1ffb2448
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="data-science-deep-dive-using-the-revoscaler-packages"></a>資料科學深入探討︰使用 RevoScaleR 套件

本教學課程示範如何使用增強的 R 封裝中提供[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]使用 SQL Server 資料，並建立可調整的 R 解決方案，做為運算環境中使用的伺服器，進行高效能巨量資料分析。

您將學習如何建立遠端計算內容中，本機和遠端計算內容之間移動資料，並在遠端 SQL Server 上執行 R 程式碼。 您也將學習如何分析和繪製的資料，包括本機或遠端伺服器，以及如何建立及部署模型。

> [!NOTE]
> 
> 本教學課程會在 Windows 中，才能存取 SQL Server 資料，並使用資料庫中的計算內容。 如果您想要在其他內容，例如 Teradata、 Linux 或是 Hadoop，使用 R，請參閱這些 Microsoft R Server 教學課程： 
> + [使用 R 伺服器，而 sparklyr](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-spark-interop)
> + [在 25 個函數中探索 R 和 ScaleR (英文)](https://msdn.microsoft.com/microsoft-r/microsoft-r-tutorial-r2revoscaler)
> + [在 Hadoop MapReduce ScaleR 快速入門](https://msdn.microsoft.com/microsoft-r/scaler-hadoop-getting-started)
> + [RevoScaleR Teradata 取得入門指南](https://msdn.microsoft.com/microsoft-r/scaler-teradata-getting-started)

## <a name="overview"></a>概觀

為了說明 ScaleR 套件的彈性和處理能力，在本教學課程中，您將會頻繁地移動資料以及交換計算內容。

+ 資料最初是從 CSV 檔案或 XDF 檔案取得。 您將使用 RevoScaleR 套件中的函數，將資料匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
+ 模型定型和計分將會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 計算內容中執行。
    您將使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rx **函數建立新的** 資料表，以儲存您的計分結果。
+ 您將在伺服器和本機計算內容中建立繪圖。
+ 為了定型模型，您將使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中已儲存的資料。 所有計算都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行。
+ 您將擷取資料子集，並將它儲存為 XDF 檔案，以便在本機工作站上重複用於分析。
+ 計分程序期間所使用的新資料是透過 ODBC 連線從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫擷取。 所有計算都會在本機工作站上執行。
+ 最後，您將使用伺服器計算內容，根據自訂 R 函數來執行模擬。

### <a name="get-started-now"></a>立即開始使用

本教學課程需要大約 75 分鐘才能完成，不包括安裝程式。

1. [使用 SQL Server 資料使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [使用 RxSqlServerData 建立 SQL Server 資料物件](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [查詢及修改 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [定義和使用的計算內容](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [建立和執行 R 指令碼](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [使用 R 的 SQL Server 資料視覺化](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [建立 R 模型](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [分數新的資料](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [使用 R 的資料轉換](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [將資料載入至使用 rxImport 記憶體](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [建立新的 SQL Server 資料表，使用 rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [執行區塊使用 rxDataStep 分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [分析本機計算內容; 中的資料](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [SQL Server 和 XDF 檔案之間移動資料](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [建立簡單的模擬](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>目標對象

本教學課程適用於或已對 R 和資料科學工作 (包括瀏覽、統計分析和模型調整) 有點熟悉的資料科學家或人員。  不過，所有的程式碼，所以即使您是新手 R，則您可以輕鬆地執行程式碼並跟著做，請假設您擁有所需的伺服器和用戶端環境。

您也應該熟悉 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法，而且知道如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或其他資料庫工具 (例如 Visual Studio) 來存取 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 資料庫。
  
> [!TIP]
> 在每堂課之間儲存 R 工作區，以輕鬆地從先前離開的地方繼續進行。

### <a name="prerequisites"></a>必要條件

- **支援 R 與 SQL Server**
  
    安裝 SQL Server 2016 並啟用 R 服務 （資料庫）。 或者，安裝 SQL Server 2017，啟用機器學習服務並選擇的 R 語言。 在安裝程序所述[SQL Server 2016 線上叢書 》](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx)。
  
-  **資料庫權限**
  
    若要執行用來定型模型的查詢，您必須具有資料儲存所在資料庫的 **db_datareader** 權限。 若要執行 R，您的使用者必須具有權限，EXECUTE ANY EXTERNAL SCRIPT。

-   **資料科學開發電腦**
  
    您也必須安裝 R 開發環境中的 RevoScaleR 封裝和相關的提供者。 若要這樣做最簡單的方式是安裝 Microsoft R 用戶端或 Microsoft R Server （獨立）。 如需詳細資訊，請參閱 [Set Up a Data Science Client](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx)(設定資料科學用戶端)。
      
    > [!NOTE] 
    > 不支援 Revolution R Enterprise 或 Revolution R Open 的其他版本。
    > 
    > R、 R 3.2.2，例如開放原始碼散發將不適用於此教學課程中，因為 RevoScaleR 函數可以使用遠端計算內容。
  
-   **其他 R 套件**
  
    在本教學課程中，您必須安裝下列套件︰ **dplyr**、 **ggplot2**、 **ggthemes**、 **reshape2**和 **e1071**。 相關指示會隨本教學課程一起提供。
  
    必須安裝所有封裝，在兩個地方： 您用於開發 R 解決方案，在電腦上，將會執行 R 指令碼的 SQL Server 電腦上。 如果您沒有在伺服器電腦上安裝封裝的權限，請要求系統管理員。 **請不要將套件安裝至使用者程式庫。** 請務必封裝會安裝 SQL Server 執行個體使用的 R 封裝文件庫中。

如需詳細資訊，請參閱[資料科學逐步解說的必要條件](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)。



## <a name="next-step"></a>下一個步驟

[使用 SQL Server 資料使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

