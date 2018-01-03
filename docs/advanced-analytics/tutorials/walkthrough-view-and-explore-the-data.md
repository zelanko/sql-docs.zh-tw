---
title: "檢視及瀏覽的資料，使用 SQL （逐步解說） |Microsoft 文件"
ms.custom: 
ms.date: 07/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: "33"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f6bf3d5ea1e1018a727f94bc2ae2682fc8f7e5e3
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="view-and-explore-the-data-using-sql-walkthrough"></a>檢視及瀏覽的資料，使用 SQL （逐步解說）

資料瀏覽是建立資料模型很重要的一部分，而且牽涉到檢視用於分析的資料物件摘要，以及資料視覺化。 在這一課中，瀏覽資料物件和產生的繪圖，兩者都使用[!INCLUDE[tsql](../../includes/tsql-md.md)]和中所含的 R 函數[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。

然後您產生一個繪圖來視覺化資料，與所安裝的套件所提供的新函式的使用[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。

> [!TIP]
> 已經是 R 大師了嗎？
>   
> 現在您已下載所有資料並備妥環境，您可以自由地在 RStudio 或任何其他環境中執行完整的 R 指令碼，並自行瀏覽功能。 只要開啟 RSQL_Walkthrough.R 檔案並反白顯示和執行每一行，或將整個指令碼當作示範來執行。
>   
> 若要取得 RevoScaleR 函數的其他說明，以及在 R 中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料的秘訣，請繼續進行本教學課程。 它會使用完全相同的指令碼。

## <a name="verify-downloaded-data-using-sql-server"></a>請確認下載的資料，使用 SQL Server

首先，花點時間確定您的資料已正確載入。

1. 連接到您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體使用您喜愛的資料庫管理工具，例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，Visual Studio 或 Visual Studio 程式碼中的伺服器總管。

2. 選取您建立，並展開以查看新的資料庫、 資料表和函式的資料庫。
  
    ![rsql_e2e_ssms_newobjects](media/rsql-e2e-ssms-newobjects.PNG)
  
3.  請確認正確地載入資料，以滑鼠右鍵按一下資料表並選取**選取前 1000 個資料列**。 功能表選項會執行這項查詢：

    ```SQL
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]
    ```
    如果您在資料表中看不到任何資料，請參閱上一個主題中的 [疑難排解](walkthrough-prepare-the-data.md) 一節。

4. 此資料表已透過加入[資料行存放區索引](../../relational-databases/indexes/columnstore-indexes-overview.md)，針對集合式計算最佳化。 執行此陳述式產生的資料表上的簡短摘要。

    ```SQL
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
    在下一課中，您會使用 R 產生一些更複雜的摘要。

## <a name="next-lesson"></a>下一課

[使用 R 的資料摘要](walkthrough-view-and-summarize-data-using-r.md)

## <a name="previous-lesson"></a>上一課

[準備要使用 PowerShell 的資料](walkthrough-prepare-the-data.md)
