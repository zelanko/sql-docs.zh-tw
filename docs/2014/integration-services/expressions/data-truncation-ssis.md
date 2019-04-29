---
title: 資料截斷 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- truncating data
- data truncation [Integration Services]
- expressions [Integration Services], data truncation
- truncate options [Integration Services]
ms.assetid: 02461e15-49ca-445b-abb3-5c369c283ec2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ce2b4a14d78c4e855c4af1d8b5fdd972b1d28c27
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62898325"
---
# <a name="data-truncation-ssis"></a>資料截斷 (SSIS)
  運算式可能不小心造成資料遭截斷。 在下列情況下可能發生截斷：  
  
-   字串。 例如，將具有 DT_WSTR 資料類型的字串資料，翻譯成具有 DT_STR 資料類型的相同長度字串 (以字元計算) 時，如果原始字串包含雙位元組字元，則會造成資料遺失。  
  
-   有效位數。 例如，將整數從 DT_I4 資料類型轉換成 DT_I2 資料類型，或將不帶正負號的整數轉換成帶正負號的整數。  
  
-   無效位數。 例如，將實數從 DT_R8 轉換成 DT_R4，或將整數從 DT_I4 資料類型轉換成 DT_R4 資料類型。  
  
 運算式評估工具會識別可能導致截斷的明確轉換，並在剖析運算式時發出警告。 例如，如果將 30 個字元的字串轉換成 20 個字元的字串，則運算式評估工具會向您發出警告。  
  
> [!NOTE]  
>  在執行階段不會檢查截斷；資料會在沒有任何警告下遭截斷。 不過，多數資料配接器和轉換支援錯誤輸出，可處理錯誤資料列的配置。 如需處理資料截斷的詳細資訊，請參閱 <<c0> [ 處理資料中的錯誤](../data-flow/error-handling-in-data.md)。  
  
  
