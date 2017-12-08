---
title: "檢視或變更模型旗標 （資料採礦） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d1169735-fb18-417b-b8d6-9a161e444020
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 98ec1ace5b819a123fd4a8949c92caa5e3be4e5f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="view-or-change-modeling-flags-data-mining"></a>檢視或變更模型旗標 (資料採礦)
  模型旗標是您針對採礦結構資料行或採礦模型資料行設定的屬性，可控制演算法如何在分析期間處理資料。  
  
 在資料採礦設計師中，您可以藉由檢視結構或模型的屬性來檢視及修改與採礦結構或採礦資料行相關聯的模型旗標。 您也可以使用 DMX、AMO 或 XMLA 來設定模型旗標。  
  
 此程序描述如何在設計工具中變更模型旗標。  
  
### <a name="view-or-change-the-modeling-flag-for-a-structure-column-or-model-column"></a>檢視或變更結構資料行或模型資料行的模型旗標  
  
1.  在 SQL Server Design Studio 中開啟 [方案總管]，然後按兩下採礦結構。  
  
2.  若要設定 NOT NULL 模型旗標，按一下 **[採礦結構]** 索引標籤。若要設定 REGRESSOR 或 MODEL_EXISTENCE_ONLY 旗標，請按一下 [採礦模型] 索引標籤。  
  
3.  以滑鼠右鍵按一下要檢視或變更的資料行，然後選取 [屬性]。  
  
4.  若要新增模型旗標，按一下 **[ModelingFlags]** 屬性，然後選取要使用之模型旗標的核取方塊。  
  
     只有適合資料行資料類型的模型旗標才會顯示。  
  
    > [!NOTE]  
    >  在變更模型旗標後，必須重新處理模型。  
  
### <a name="get-the-modeling-flags-used-in-the-model"></a>取得模型中使用的模型旗標  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中開啟 [DMX 查詢] 視窗，然後輸入類似以下的查詢：  
  
    ```  
    SELECT COLUMN_NAME, CONTENT_TYPE, MODELING_FLAG  
    FROM $system.DMSCHEMA_MINING_COLUMNS  
    WHERE MODEL_NAME = 'Forecasting'  
  
    ```  
  
## <a name="see-also"></a>請參閱＜  
 [採礦模型工作和使用說明](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [模型旗標 &#40;資料採礦&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  
