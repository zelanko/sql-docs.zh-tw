---
title: "變更資料採礦查詢的逾時值 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time-out
ms.assetid: f1add4bc-e882-440a-a98b-333cfa274c3e
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 51603c1919fae5e164348181412712d4dfc673a0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>針對資料採礦查詢變更逾時值
  在建立增益圖或執行預測查詢時，有時可能要花很長的時間才能產生預測所需的所有資料。 若要避免查詢逾時，可以變更控制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器等候完成查詢多久時間的值。  
  
 預設值為 15；不過，如果模型很複雜，或者資料來源很龐大，則這樣的時間長度可能不夠。 如有必要，可以大幅增加此值，以提供足夠的時間進行處理。 例如，如果將 **[查詢逾時]** 設定為 600，則查詢可能會持續執行長達 10 分鐘。  
  
 如需預測查詢的詳細資訊，請參閱 [資料採礦查詢工作和使用說明](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)。  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>設定資料採礦查詢的逾時值  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，從 **[工具]** 功能表選取 **[選項]**。  
  
2.  在 **[選項]** 窗格中，展開 **[商業智慧設計師]**。  
  
3.  按一下 **[查詢逾時]** 文字方塊，並輸入秒數的值。  
  
## <a name="see-also"></a>請參閱＜  
 [資料採礦查詢工作和使用說明](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
