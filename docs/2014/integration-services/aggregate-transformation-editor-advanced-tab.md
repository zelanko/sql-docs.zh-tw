---
title: 匯總轉換編輯器（[Advanced] 索引標籤） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregationtransformation.advanced.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: 186a9736-2554-40a0-9cb2-877a8db5fde8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c437e15cbbcb3df64770ad0da4272eedf41cf0e9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439485"
---
# <a name="aggregate-transformation-editor-advanced-tab"></a>彙總轉換編輯器 (進階索引標籤)
  使用 **[彙總轉換編輯器]** 對話方塊的 **[進階]** 索引標籤，即可設定元件屬性、指定彙總，以及設定輸入和輸出資料行的屬性。  
  
> [!NOTE]  
>  索引鍵計數、索引鍵小數位數、相異索引鍵計數和相異索引鍵小數位數的選項，若是指定在 [進階]**** 索引標籤上，就會套用至元件層級；若是指定在 [彙總]**** 索引標籤的進階畫面上，則會套用至輸出層級；若是指定在 [彙總]**** 索引標籤底端的資料行清單中，則會套用至資料行層級。  
>   
>  在彙總轉換中， **[索引鍵]** 和 **[索引鍵小數位數]** 會參考預期要從 **[群組依據]** 作業產生的群組數。 **[計算相異索引鍵]** 和 **[計算相異小數位數]** 會參考預期要從 **[相異計數]** 作業產生的相異值數目。  
  
 若要了解有關彙總轉換的詳細資訊，請參閱＜ [Aggregate Transformation](data-flow/transformations/aggregate-transformation.md)＞。  
  
## <a name="options"></a>選項  
 **[索引鍵小數位數]**  
 選擇性地指定彙總預期的近似索引鍵數目。 轉換時會使用此資訊來最佳化初始快取大小。 根據預設，此選項的值為 **[未指定]**。 如果 **[索引鍵小數位數]** 和 **[索引鍵數目]** 都有指定，會優先使用 **[索引鍵數目]** 。  
  
|值|描述|  
|-----------|-----------------|  
|[未指定]|不使用 **[索引鍵小數位數]** 屬性。|  
|低|彙總可寫入大約 500,000 個索引鍵。|  
|中|彙總可寫入大約 5,000,000 個索引鍵。|  
|高|彙總可寫入超過 25,000,000 個索引鍵。|  
  
 **金鑰數目**  
 選擇性地指定彙總預期的確實索引鍵數目。 轉換時會使用此資訊來最佳化初始快取大小。 如果 **[索引鍵小數位數]** 和 **[索引鍵數目]** 都有指定，會優先使用 **[索引鍵數目]** 。  
  
 **[計算相異小數位數]**  
 可選擇性地指定彙總可寫入之相異值的近似數目。 根據預設，此選項的值為 **[未指定]**。 如果 **[計算相異小數位數]** 和 **[計算相異索引鍵]** 都有指定，會優先使用 **[計算相異索引鍵]** 。  
  
|值|描述|  
|-----------|-----------------|  
|[未指定]|不使用 CountDistinctScale 屬性。|  
|低|彙總可寫入大約 500,000 個相異值。|  
|中|彙總可寫入大約 5,000,000 個相異值。|  
|高|彙總可寫入超過 25,000,000 個相異值。|  
  
 **[計算相異索引鍵]**  
 可選擇性地指定彙總可寫入之相異值的確實數目。 如果 **[計算相異小數位數]** 和 **[計算相異索引鍵]** 都有指定，會優先使用 **[計算相異索引鍵]** 。  
  
 **自動擴充因數**  
 使用介於 1 到 100 之間的值，指定記憶體於彙總期間可以擴充的百分比。 根據預設，此選項的值為 **25%**。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [匯總轉換編輯器 &#40;匯總] 索引標籤&#41;](../../2014/integration-services/aggregate-transformation-editor-aggregations-tab.md)   
 [使用彙總轉換來彙總資料集中的值](data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  
