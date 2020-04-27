---
title: 查看並儲存預測查詢的結果 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- prediction queries [Analysis Services]
- viewing prediction query results
- displaying prediction query results
- Mining Model Prediction [Analysis Services], viewing results
ms.assetid: abba4d24-3619-44c1-8279-88f27ad627d3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9abaf092d00a8acaf6c0b3ef963c940199068ce9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082705"
---
# <a name="view-and-save-the-results-of-a-prediction-query"></a>檢視及儲存預測查詢的結果
  在中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]使用預測查詢產生器定義查詢之後，您可以藉由切換至 [查詢結果] 視圖來執行查詢並查看結果。  
  
 您可以將預測查詢的結果儲存至[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案中所定義之任何資料來源中的資料表。 您可以建立新的資料表，或將查詢結果儲存至現有的資料表。 如果您將結果儲存至現有的資料表，則可選擇覆寫目前儲存在資料表中的資料，否則查詢結果會附加至資料表中的現有資料。  
  
### <a name="run-a-query-and-view-the-results"></a>執行查詢並檢視結果  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，於資料採礦設計師之 [採礦模型預測]**** 索引標籤的工具列上，按一下 [結果]****。  
  
     查詢結果檢視會開啟並執行查詢。 結果會顯示在檢視器的方格中。  
  
### <a name="save-the-results-of-a-prediction-query-to-a-table"></a>將預測查詢的結果儲存至資料表  
  
1.  在資料採礦設計師之 [採礦模型預測]**** 索引標籤的工具列上，按一下 [儲存查詢結果]****。  
  
     [儲存資料採礦查詢結果]**** 對話方塊隨即開啟。  
  
2.  從 [資料來源]**** 清單中選取資料來源，或按一下 [新增]**** 來建立新的資料來源。  
  
3.  在 [資料表名稱]**** 方塊中，輸入資料表的名稱。 如果資料表已存在，請選取 [如果存在則覆寫]****，即可將資料表的內容取代成查詢結果。 如果您不想要覆寫資料表的內容，請勿選取此核取方塊。 新查詢結果將附加至資料表中的現有資料。  
  
4.  如果您想要將資料表加入資料來源檢視，請從 [加入至 DSV]**** 中選取資料來源檢視。  
  
5.  按一下 **[儲存]** 。  
  
    > [!WARNING]  
    >  如果目的地不支援階層式資料列集，您可以將 FALTTENED 關鍵字加入至結果中，以便儲存為二維資料表。  
  
  
