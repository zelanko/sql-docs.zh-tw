---
title: "聯集全部 」 轉換 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.unionalltrans.f1
- sql13.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: e947aa8b3d079830b9433ba1b01450fda699904a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/19/2017

---
# <a name="union-all-transformation"></a>聯集全部轉換
  「聯集全部」轉換會將多項輸入結合至單一輸出。 例如，五個不同的「一般檔案」來源的輸出，可做為「聯集全部」轉換的輸入並組合成一個輸出。  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 轉換輸入會逐一加入至轉換輸出；不會發生任何重新排列資料列的情形。 如果封裝需要經過排序的輸出，則您應使用「合併」轉換而非「聯集全部」轉換。  
  
 您連接到「聯集全部」轉換的第一個輸入，是轉換從中建立轉換輸出的輸入。 您接著連接到轉換的輸入中的資料行，會對應至轉換輸出中的資料行。  
  
 若要合併輸入，請將輸入中的資料行對應至輸出中的資料行。 您至少必須將一個輸入的資料行對應至各輸出資料行。 兩個資料行之間的對應，會要求資料行的中繼資料相符。 例如，對應的資料行必須擁有相同的資料類型。  
  
 如果對應的資料行包含字串資料，而輸出資料行的長度比輸入資料行短，則輸出資料行的長度會自動增加，以包含輸入資料行。 未對應至輸出資料行的輸入資料行會在輸出資料行中設為 Null 值。  
  
 此轉換有多個輸入和一個輸出。 它不支援錯誤輸出。  
  
## <a name="configuration-of-the-union-all-transformation"></a>聯集全部轉換的組態  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可透過程式設計方式設定之屬性的詳細資訊，請參閱 [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)。  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="union-all-transformation-editor"></a>聯集全部轉換編輯器
  使用 **[聯集全部轉換編輯器]** 對話方塊，即可將數個輸入資料列集合併至單一輸出資料列集。 藉由在資料流程中包含聯集全部轉換，您可以合併多個資料流程中的資料、藉由巢狀聯集全部轉換來建立複雜資料集、以及更正資料中的錯誤之後重新合併資料列。  
  
### <a name="options"></a>選項  
 **輸出資料行名稱**  
 輸入每個資料行的別名。 預設值為第一個 (參考) 輸入的輸入資料行名稱；不過，您也可以選擇任何唯一的、描述性的名稱。  
  
 **聯集全部輸入 1**  
 從第一個 (參考) 輸入的可用輸入資料行清單中選取。 對應資料行的中繼資料必須相符。  
  
 **聯集全部輸入 n**  
 從第二個和其他輸入的可用輸入資料行清單中選取。 對應資料行的中繼資料必須相符。  
  
## <a name="related-tasks"></a>相關工作  
 [使用聯集全部轉換來合併資料](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  

