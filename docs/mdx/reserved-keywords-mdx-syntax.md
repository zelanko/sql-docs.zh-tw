---
title: 保留的關鍵字 （MDX 語法） |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2f50b0292b9139dcbb2b3a5652ad41136b31702a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742627"
---
# <a name="reserved-keywords-mdx-syntax"></a>保留的關鍵字 (MDX 語法)


  Analysis Services 會保留為專用的特定關鍵字。 如需保留關鍵字的清單，請參閱[MDX 保留字](../mdx/mdx-reserved-words.md)。  
  
 保留關鍵字會遵循這些指導方針：  
  
-   除了由 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 定義的位置之外，您無法在多維度運算式 (MDX) 陳述式中的任何位置包括保留關鍵字 。  
  
-   資料庫的物件名稱不得與保留關鍵字完全相同。 如果有這種名稱，則必須使用分隔識別碼來參考物件。 雖然這個方法確實允許物件名稱作為保留關鍵字，但還是應該避免使用關鍵字來命名物件。  
  
-   使用會避免用到保留關鍵字的命名慣例。 如果物件名稱必須看起來像保留關鍵字，您可移除子音或母音。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 語法元素&#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
