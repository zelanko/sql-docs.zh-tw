---
title: 查看或變更模型旗標（資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d1169735-fb18-417b-b8d6-9a161e444020
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7657e7502d3b215cd87326c51cc9416ba0707235
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082683"
---
# <a name="view-or-change-modeling-flags-data-mining"></a>檢視或變更模型旗標 (資料採礦)
  模型旗標是您針對採礦結構資料行或採礦模型資料行設定的屬性，可控制演算法如何在分析期間處理資料。  
  
 在資料採礦設計師中，您可以藉由檢視結構或模型的屬性來檢視及修改與採礦結構或採礦資料行相關聯的模型旗標。 您也可以使用 DMX、AMO 或 XMLA 來設定模型旗標。  
  
 此程序描述如何在設計工具中變更模型旗標。  
  
### <a name="view-or-change-the-modeling-flag-for-a-structure-column-or-model-column"></a>檢視或變更結構資料行或模型資料行的模型旗標  
  
1.  在 SQL Server Design Studio 中開啟 [方案總管]，然後按兩下採礦結構。  
  
2.  若要設定 NOT Null 模型旗標，請按一下 [**採礦結構**] 索引標籤。若要設定回歸輸入變數或 MODEL_EXISTENCE_ONLY 旗標，請按一下 [**採礦模型**] 索引標籤。  
  
3.  以滑鼠右鍵按一下要檢視或變更的資料行，然後選取 [屬性]****。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [採礦模型工作和操作說明](mining-model-tasks-and-how-tos.md)   
 [資料採礦&#41;的模型旗標 &#40;](modeling-flags-data-mining.md)  
  
  
