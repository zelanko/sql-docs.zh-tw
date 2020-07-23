---
title: 保留關鍵字（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6359b17825e1f62c38492acb6747ca52a264c7bc
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970625"
---
# <a name="reserved-keywords-dmx"></a>保留關鍵字 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]保留特定關鍵字供其獨佔使用。 這些關鍵字只能用於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在資料採礦延伸模組 (DMX) 語言參考中定義的位置，不能用於 DMX 陳述式中其他任何地方。 這些限制 DMX 關鍵字包括下列成員：  
  
-   在[DMX 資料定義語句](../dmx/dmx-statements-data-definition.md)主題中列出的所有資料定義語句。  
  
-   在[DMX 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)主題中列出的所有資料採礦查詢函數。  
  
-   在[DMX 運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)主題中列出的所有運算子。  
  
-   定義於多維度運算式 (MDX) 查詢語言中，且併入當做 DMX 陳述式之一部分的關鍵字。  
  
-   定義於 OLE DB for Data Mining 規格中，且併入當做 DMX 陳述式之一部分的關鍵字。  
  
 您為資料庫中的物件命名時，建議您使用能避免用到保留關鍵字的命名慣例。  
  
 如果您的資料庫包含與保留關鍵字相符的名稱，則在參考這些物件時必須使用分隔識別碼。 如需詳細資訊，請參閱[DMX&#41;&#40;的識別碼](../dmx/identifiers-dmx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 語法元素的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
