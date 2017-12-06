---
title: "SQL Server R 教學課程 |Microsoft 文件"
ms.custom: SQL2016_New_Updated
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ee88d7dbbb1a10c11a1e1c50cb4c048189f9d026
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="sql-server-r-tutorials"></a>SQL Server R 教學課程

本文提供教學課程和範例，示範如何使用 R 與 SQL Server 2016 或 SQL Server 2017 的清單。 透過這些範例和示範中，您將學習：

+ 如何從 T-SQL 執行 R
+ 遠端和本機計算內容和您可以執行 R 程式碼使用 SQL Server 電腦的方式為何
+ 如何將 R 程式碼包裝在預存程序
+ 最佳化 SQL 生產環境中的 R 程式碼
+ 內嵌在應用程式中的機器學習的真實世界案例

如需需求和安裝資訊，請參閱[必要條件](#bkmk_Prerequisites)。

## <a name="bkmk_sqltutorials"></a>R 教學課程

除非另行指定，教學課程所開發的 SQL Server 2016 R 服務，而且不重大變更適用於 SQL Server 2017 機器學習服務。

所有教學課程會大量使用 RevoScaleR 封裝中的功能適用於 SQL Server 計算內容。

+ [使用 R 和 SQL Server 資料科學深入探討](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

  了解如何使用 RevoScaleR 封裝中的函式。 R 與 SQL Server 和參數之間移動資料計算以符合特定工作的內容。 建立模型和繪圖，和您的開發環境和資料庫伺服器之間移動它們。

  **對象：**資料科學家或開發人員已熟悉 R 語言中，而且想要深入了解增強的 R 封裝以及由 Revolution Analytics 的 Microsoft R 中的函式。

  **需求：**一些基本的 R 知識。 使用 SQL Server R 服務或機器學習服務的 r 伺服器的存取權安裝程式說明，請參閱[必要條件](#bkmk_Prerequisites)。

+ [資料庫中的 SQL 開發人員的 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

  建置和部署完整的 R 解決方案，僅限使用[!INCLUDE[tsql](../../includes/tsql-md.md)]工具。

  著重於將方案移到實際執行環境。 您將了解如何將 R 程式碼包裝在預存程序中、將 R 模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，以及對 R 模型進行參數化呼叫來進行預測。

  **對象：** SQL 開發人員、 應用程式開發人員，或 SQL 專業人員支援 R 解決方案，而且想要了解如何將 R 模型部署到 SQL Server。

  **需求：**任何 R 環境所需。 提供所有的 R 程式碼，而且可以建置完整的解決方案只使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]和熟悉的商務智慧和 SQL 開發工具。 不過，R 的一些基本的知識會很有幫助。

  您必須安裝並啟用之 R 語言 SQL 伺服器的存取權。 安裝程式說明，請參閱[必要條件](#bkmk_Prerequisites)。

+ [快速入門： 在 T-SQL 中使用 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

  本快速入門涵蓋使用 R 中的基本語法[!INCLUDE[tsql](../../includes/tsql-md.md)]。

  了解如何從 T-SQL 呼叫 R 執行階段、 將 R 函式包裝在 SQL 程式碼，以及執行將 R 輸出與 R 模型儲存至 SQL 資料表的預存程序。

  **對象：**為人熟悉的功能，以及想要了解從預存程序呼叫 R 的基本概念。

  **需求：** R 或 SQL 所需的任何知識。 不過，您需要 SQL Server Management Studio 或其他用戶端可以連接到資料庫並執行 T-SQL。 我們建議您免費[MSSQL 擴充 Visual Studio 程式碼](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)如果您不熟悉 T-SQL 查詢。

  您也必須與 SQL Server R 服務或機器學習服務，使用已啟用的 R 伺服器的存取權。 安裝程式說明，請參閱[必要條件](#bkmk_Prerequisites)。

+ [資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

  示範資料科學程序從開始到結束時，取得資料並將它儲存到 SQL Server、 分析使用 R 資料與建置圖形。

  您將學習如何移動圖形之間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 R 和 T-SQL 中 R 函數的比較特徵設計。 最後，您將學習如何使用中的預測模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]批次計分和計分單一資料列。

  **對象：**人士熟悉 R 與 SQL Server Management Studio 之類的開發人員工具。

  **需求：**您應該可以存取的 R 開發環境，而且知道如何執行 R 指令。 使用 PowerShell，才能下載 New York City 計程車資料集。 您必須使用 SQL Server R 服務或機器學習服務，使用已啟用的 R 伺服器的存取權。 安裝程式說明，請參閱[必要條件](#bkmk_Prerequisites)。

## <a name ="bkmk_samples"></a>產品範例

SQL Server 開發團隊，以反白顯示您可以在真實世界應用程式中使用內嵌的分析是有許多方法會提供這些範例和示範。

+ [建置使用 R 和 SQL Server 的預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  了解 ski 以租用方式佔用企業可能會使用機器學習來預測未來出租，它可以幫助商務計劃和人員，以符合未來的要求。

+ [執行客戶群集使用 R 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  使用不受監督的學習，根據銷售資料的區段客戶。

## <a name="bkmk_Prerequisites"></a>必要條件

若要使用這些教學課程和範例，您必須安裝下列伺服器產品的其中一個：

+ SQL Server 2016 R 服務 （資料庫）
  
  支援。 請務必安裝機器學習功能，然後再啟用 外部指令碼。

+ SQL Server 2017 機器學習服務 （資料庫）
  
  支援 R 或 Python。 您必須選取的機器學習功能和語言，若要安裝，然後再啟用 外部指令碼。

執行 SQL Server 安裝程式，別忘了下列重要步驟：

+ 執行啟用外部指令碼執行功能`sp_configure 'external scripts enabled', 1`
+ 重新啟動伺服器
+ 請確定呼叫外部執行階段的服務具有必要權限
+ 請確認您的 SQL 登入或 Windows 使用者帳戶具有必要權限連接到伺服器，來讀取資料，並建立此範例所需的任何資料庫物件

如果您遇到問題，請參閱本文章的一些常見問題：[疑難排解機器學習服務](../machine-learning-troubleshooting-faq.md)
