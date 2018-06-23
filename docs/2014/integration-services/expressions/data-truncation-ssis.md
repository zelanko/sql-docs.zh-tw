---
title: 資料截斷 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- truncating data
- data truncation [Integration Services]
- expressions [Integration Services], data truncation
- truncate options [Integration Services]
ms.assetid: 02461e15-49ca-445b-abb3-5c369c283ec2
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e735659fb2898c2ab6bc428d7ad6fc0f5759f17c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134220"
---
# <a name="data-truncation-ssis"></a>資料截斷 (SSIS)
  運算式可能不小心造成資料遭截斷。 在下列情況下可能發生截斷：  
  
-   字串。 例如，將具有 DT_WSTR 資料類型的字串資料，翻譯成具有 DT_STR 資料類型的相同長度字串 (以字元計算) 時，如果原始字串包含雙位元組字元，則會造成資料遺失。  
  
-   有效位數。 例如，將整數從 DT_I4 資料類型轉換成 DT_I2 資料類型，或將不帶正負號的整數轉換成帶正負號的整數。  
  
-   無效位數。 例如，將實數從 DT_R8 轉換成 DT_R4，或將整數從 DT_I4 資料類型轉換成 DT_R4 資料類型。  
  
 運算式評估工具會識別可能導致截斷的明確轉換，並在剖析運算式時發出警告。 例如，如果將 30 個字元的字串轉換成 20 個字元的字串，則運算式評估工具會向您發出警告。  
  
> [!NOTE]  
>  在執行階段不會檢查截斷；資料會在沒有任何警告下遭截斷。 不過，多數資料配接器和轉換支援錯誤輸出，可處理錯誤資料列的配置。 如需處理資料截斷的詳細資訊，請參閱[Error Handling in Data](../data-flow/error-handling-in-data.md)。  
  
  