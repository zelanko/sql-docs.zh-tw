---
title: 變更資料採礦查詢的超時值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time-out
ms.assetid: f1add4bc-e882-440a-a98b-333cfa274c3e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 640d07115e2a071bb5d57e87955c11670f4c38b0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66085884"
---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>針對資料採礦查詢變更逾時值
  在建立增益圖或執行預測查詢時，有時可能要花很長的時間才能產生預測所需的所有資料。 若要避免查詢逾時，可以變更控制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器等候完成查詢多久時間的值。  
  
 預設值為 15；不過，如果模型很複雜，或者資料來源很龐大，則這樣的時間長度可能不夠。 如有必要，可以大幅增加此值，以提供足夠的時間進行處理。 例如，如果將 **[查詢逾時]** 設定為 600，則查詢可能會持續執行長達 10 分鐘。  
  
 如需預測查詢的詳細資訊，請參閱 [資料採礦查詢工作和使用說明](data-mining-query-tasks-and-how-tos.md)。  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>設定資料採礦查詢的逾時值  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，從 **[工具]** 功能表選取 **[選項]**。  
  
2.  在 **[選項]** 窗格中，展開 **[商業智慧設計師]**。  
  
3.  按一下 **[查詢逾時]** 文字方塊，並輸入秒數的值。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦查詢工作和操作說明](data-mining-query-tasks-and-how-tos.md)   
 [資料採礦查詢](data-mining-queries.md)  
  
  
