---
title: 模糊群組轉換編輯器 （進階索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: dd820d75-b8a7-4515-aea4-3553ba5b442e
caps.latest.revision: 28
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7e8c12ad683e46838a88359170ea970f20c02828
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231518"
---
# <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>模糊群組轉換編輯器 (進階索引標籤)
  使用 **[模糊群組轉換編輯器]** 對話方塊的 **[進階]** 索引標籤，即可指定輸入和輸出資料行、設定類似度臨界值，以及定義分隔符號。  
  
> [!NOTE]  
>  `Exhaustive`而`MaxMemoryUsage`模糊群組轉換的屬性不適用於**模糊群組轉換編輯器**，但可以透過設定**進階編輯器**. 如需有關這些屬性的詳細資訊，請參閱＜ [Transformation Custom Properties](data-flow/transformations/transformation-custom-properties.md)＞的「模糊群組轉換」一節。  
  
 若要深入了解模糊群組轉換，請參閱＜ [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **輸入索引鍵資料行名稱**  
 針對每個輸入資料列，指定包含資料列之唯一識別碼的輸出資料行名稱。 `_key_in`資料行具有唯一識別每個資料列的值。  
  
 **輸出索引鍵資料行名稱**  
 針對由一組重複資料列組成的標準資料列，指定包含標準資料列之唯一識別碼的輸出資料行名稱。 `_key_out` 資料行會對應至標準資料之資料列的 `_key_in` 值。  
  
 **相似度分數資料行名稱**  
 指定包含相似度分數之資料行的名稱。 相似度分數是介於 0 與 1 的值，以表示輸入資料列與標準資料列的相似度。 分數愈接近於 1，資料列與標準資料列的相符程度就愈高。  
  
 **相似度臨界值**  
 使用滑桿來設定相似度臨界值。 臨界值越接近 1，資料列就必須彼此更相似才能判定為重複。 增加臨界值可以改善比對的速度，因為需要考慮的候選記錄比較少。  
  
 **Token 分隔符號**  
 此項轉換提供了 Token 化資料所用的預設分隔符號集，但您可以依需要編輯清單來新增或移除分隔符號。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用模糊群組轉換來識別相似的資料列](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
