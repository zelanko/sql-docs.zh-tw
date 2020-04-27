---
title: 模糊群組轉換編輯器（資料行索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.columns.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 24f4539f-2a9f-4acd-acc7-06228a07f7df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a97225797380294968f1af595f1299e478d548d3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058360"
---
# <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>模糊群組轉換編輯器 (資料行索引標籤)
  使用 **[模糊群組轉換編輯器]** 對話方塊的 **[資料行]** 索引標籤，即可指定用於將具有重複值之資料列分組的資料行。  
  
 若要深入了解模糊群組轉換，請參閱＜ [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **可用的輸入資料行**  
 從清單中選取輸入資料行，即可依據該資料行將具有重複值的資料列分組。  
  
 **名稱**  
 檢視可用之輸入資料行的名稱。  
  
 **通過**  
 選取轉換的輸出是否包含輸入資料行。 用來分組的所有資料行，都會自動複製到輸出。 您可以核取此資料行來包含其他資料行。  
  
 **輸入資料行**  
 選取先前在 [可用的輸入資料行]**** 清單中選取的其中一個輸入資料行。  
  
 **輸出別名**  
 輸入對應之輸出資料行的描述性名稱。 依預設，輸出資料行的名稱會與輸入資料行的名稱相同。  
  
 **群組輸出別名**  
 輸入資料行的描述性名稱，資料行包含已分組重複項目的標準值。 此輸出資料行的預設名稱，是輸入資料行的名稱後面附加「_clean」。  
  
 **比對類型**  
 選取模糊相符或完全相符。 如果資料列在具有模糊比對類型的所有資料行之間非常相似，資料列才會被視為重複項目。 如果您同時在特定資料行上指定完全相符，則只有當需要完全相符之資料行中的資料列值完全相同時，資料列才會被視為可能重複的項目。 因此，如果您知道特定資料行不會有錯誤或不一致的情形，就可以在該資料行上指定完全相符，以提高其他資料行的模糊比對精確度。  
  
 **最小相似度**  
 使用滑桿設定聯結層級的相似度臨界值。 此值越接近 1，查閱值與來源值的相似度必須越接近才能認定為相符。 增加臨界值可改善比對速度，因為需要考慮的候選記錄越少。  
  
 **相似度輸出別名**  
 指定新輸出資料行的名稱，此資料行包含所選取聯結的相似度分數。 如果您將此值保留空白，就不會建立輸出資料行。  
  
 **數字**  
 指定比較資料行資料時，開頭和尾端數字的顯著性。 例如，假設開頭數字屬於顯著，則 "123 Main Street" 和 "456 Main Street" 將不會被分到相同的群組中。  
  
|值|描述|  
|-----------|-----------------|  
|**兩者皆非**|開頭和尾端數字皆屬於不顯著。|  
|**開頭**|僅開頭數字屬於顯著。|  
|**尾端**|僅尾端數字屬於顯著。|  
|**LeadingAndTrailing**|開頭和尾端數字皆屬於顯著。|  
  
 **比較旗標**  
 如需字串比較選項的資訊，請參閱 [比較字串資料](data-flow/comparing-string-data.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用模糊群組轉換來識別相似的資料列](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
