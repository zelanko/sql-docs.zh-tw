---
title: 聯集全部轉換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unionalltrans.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b65e6f445ef82b3ee2bd5a06a63b031e6d884d1f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939229"
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
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [聯集全部轉換編輯器]**** 對話方塊中設定之屬性的詳細資訊，請參閱[聯集全部轉換編輯器](../../union-all-transformation-editor.md)。  
  
 如需可透過程式設計方式設定之屬性的詳細資訊，請參閱 [通用屬性](../../common-properties.md)。  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>相關工作  
 [使用聯集全部轉換來合併資料](union-all-transformation.md)  
  
  
