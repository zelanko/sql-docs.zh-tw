---
title: "選擇精確度圖表類型及設定圖表選項 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services]
- mining models [Analysis Services], validating
- classification accuracy [data mining]
- accuracy testing [data mining]
ms.assetid: bd24dd4a-624f-478a-9c94-b1361e857680
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dd7b16d8d707b05a57313c526ec721083d610db3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="choose-an-accuracy-chart-type-and-set-chart-options"></a>選擇精確度圖表類型及設定圖表選項
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供多種方法來判斷採礦模型的有效性。 您可以為每一個模型或結構建立之精確度圖表的類型取決於以下因素：  
  
-   建立模型時所使用的演算法類型  
  
-   可預測屬性的資料類型  
  
-   要測量之可預測屬性的數目  
  
 本主題提供不同精確度圖表的概觀。  
  
 **注意** ：圖表及其定義並不會儲存。 如果將包含圖表的視窗關閉，則必須再次建立該圖表。  
  
## <a name="accuracy-chart-types"></a>精確度圖表類型  
 根據您選擇的圖表類型而定，您將能夠進一步設定選項、瀏覽圖表，或是將圖表複製到剪貼簿，然後在 Excel 中處理資料。  
  
#### <a name="lift-chart"></a>增益圖  
 在設定模型及測試資料的選項後，請按一下 [增益圖] 索引標籤來檢視結果。 您也可以將圖表複製到剪貼簿，或是在 [採礦圖例] 中檢視個別趨勢線或資料點的詳細資料。  
  
#### <a name="profit-chart"></a>收益圖  
 在設定模型及測試資料的選項後，請按一下 [增益圖] 索引標籤，然後從 [圖表類型] 清單中選取 [收益圖] 來設定收益圖選項，再按一下 [確定] 檢視結果。  
  
 您可以視需要多次使用 [收益圖設定] 對話方塊，嘗試不同的成本選項及重新顯示圖表。 採礦圖例會包含有關每一個模型之預估收益的詳細資訊。 您也可以將圖表和 [採礦圖例] 的內容複製到剪貼簿，在 Excel 中進行處理。  
  
#### <a name="scatter-plot"></a>散佈圖  
 如果您選取了適當的模型類型，則當您按一下 [增益圖] 索引標籤時，圖表類型會自動設定為 [散佈圖]，然後顯示散佈圖。 將無法進行進一步的組態設定。 您也可以將圖表複製到剪貼簿，然後以圖形的形式將圖表貼到 Excel 或另一個應用程式中。  
  
#### <a name="classification-matrix"></a>分類矩陣  
 如果是分類矩陣，請使用 [輸入選擇] 索引標籤來選擇模型及測試資料，然後按一下 [分類矩陣] 索引標籤來檢視結果。  
  
 所有模型類型的分類矩陣內容都相同且無法設定。 您可以將圖表中的資料複製到剪貼簿，然後在 Excel 中進行處理。  
  
#### <a name="cross-validation-report"></a>交叉驗證報表  
 如果是交叉驗證報表，當您在方案總管中選取採礦結構或採礦模型之後，請按一下 [交叉驗證] 索引標籤、設定所有相關的選項，然後按一下 [取得結果] 來產生報表。 將無法進行進一步的組態設定。  
  
 所有模型類型的交叉驗證報表格式都相同，且無法設定。 但是，報表的內容會因您分析的模型類型以及可預測屬性的資料類型而異。 您也可以將報表的結果複製到剪貼簿，然後在 Excel 中處理資料。  
  
  
