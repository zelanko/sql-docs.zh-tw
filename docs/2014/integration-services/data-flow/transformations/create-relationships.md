---
title: 建立關聯性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.createrelationships.f1
ms.assetid: 6ebd305f-ffd2-4a1d-b24c-e28c151b94f5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 647fa27d872829a60d32c0cdc7686938ae796f2a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377646"
---
# <a name="create-relationships"></a>建立關聯性
  使用 **[建立關聯性]** 對話方塊，即可編輯來源資料行與查閱資料表資料行之間的對應，而這些資料行是在模糊查閱轉換編輯器、查閱轉換編輯器和詞彙查閱轉換編輯器中進行設定。  
  
> [!NOTE]  
>  從詞彙查閱轉換編輯器中叫用時，[建立關聯性] 對話方塊只會顯示 [輸入資料行] 和 [查閱資料行] 清單。  
  
 若要深入了解使用 **[建立關聯性]** 對話方塊的轉換，請參閱＜ [Fuzzy Lookup Transformation](lookup-transformation.md)＞、＜ [Lookup Transformation](lookup-transformation.md)＞和＜ [Term Lookup Transformation](term-lookup-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **輸入資料行**  
 從可用的輸入資料行清單中選取。  
  
 **查閱資料行**  
 從可用的查閱資料行清單中選取。  
  
 **對應類型**  
 選取模糊相符或完全相符。  
  
 當您使用模糊比對時，如果所有含模糊相符類型的資料行都具有足夠的相似度，則這些資料列就會被視為重複。 若要從模糊比對取得較佳的結果，您可以指定某些資料行應使用完全相符而非模糊比對。 例如，若您知道特定資料行沒有錯誤或不一致性，您就可以在該資料行指定完全相符，使得此資料行中只有包含相同值的資料列才會被視為可能重複。 這可在其他資料行增加模糊比對的精確度。  
  
 **比較旗標**  
 如需字串比較選項的相關資訊，請參閱 [比較字串資料](../comparing-string-data.md)。  
  
 **最小相似度**  
 藉由使用滑桿，在資料行層級設定相似度臨界值。 這個值愈接近 1，則查閱值與來源值就必須愈相似，才能認定它們相符。 增加臨界值可以改善比對的速度，因為需要考慮的候選記錄比較少。  
  
 **相似度輸出別名**  
 指定新輸出資料行的名稱，資料行中包含該選取資料行的相似度分數。 如果您將此值保留空白，就不會建立輸出資料行。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../integration-services-error-and-message-reference.md)   
 [模糊查閱轉換編輯器 &#40;資料行索引標籤&#41;](../../fuzzy-lookup-transformation-editor-columns-tab.md)   
 [查閱轉換編輯器 &#40;資料行頁面&#41;](../../lookup-transformation-editor-columns-page.md)   
 [詞彙查閱轉換編輯器 &#40;詞彙查閱索引標籤&#41;](../../term-lookup-transformation-editor-term-lookup-tab.md)  
  
  
