---
title: 識別碼（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e9dfbe291c1aa7d856862de54ed10c845b4e5544
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670393"
---
# <a name="identifiers-dmx"></a>識別碼 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  中的所有物件都 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 必須有識別碼。 物件的名稱是其識別碼。 伺服器、資料庫與資料庫物件 (例如資料來源、資料來源檢視、Cube、維度、採礦模型等等) 都有識別碼。  
  
 資料採礦延伸模組 (DMX) 中有兩個類別的識別碼：  
  
-   [一般識別碼](#RegularIdentifiers)  
  
-   [分隔識別碼](#DelimitedIdentifiers)  
  
 物件識別碼是在您定義物件時建立的。 然後您使用識別碼參考物件。 識別碼必須小於或等於 100 個字元。  
  
##  <a name="regular-identifiers"></a><a name="RegularIdentifiers"></a>一般識別碼  
 DMX 中的一般識別碼符合 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的識別碼格式規則。 DMX 中的一般識別碼不需要分隔符號。 下列是使用一般、非分隔識別碼之 DMX 陳述式的範例：  
  
```  
SELECT * FROM Clustering.CONTENT;  
```  
  
### <a name="rules-for-regular-identifiers"></a>一般識別碼的規則  
 下列是一般識別碼的格式規則：  
  
1.  一般識別碼的第一個字元必須是下列其中之一：  
  
    -   Unicode 標準2.0 所定義的字母。 包括從 a 到 z 與從 A 到 Z 的拉丁文字元，以及其他語言的字母字元。  
  
    -   底線 (_)。  
  
2.  後續的字元可以是：  
  
    -   Unicode 標準2.0 中所定義的字母。  
  
    -   其他基本拉丁文或其他國家 (地區) 字集中的十進位數字。  
  
    -   底線 (_)。  
  
3.  識別碼不可以是 DMX 保留字。 DMX 中的保留字不區分大小寫。 如需詳細資訊，請參閱[&#40;DMX&#41;的保留關鍵字](../dmx/reserved-keywords-dmx.md)。  
  
4.  識別碼不能包含內嵌空格或特殊字元。  
  
 在 DMX 陳述式中使用不符合這些規則的任何識別碼時，必須以方括號分隔這些識別碼。  
  
##  <a name="delimited-identifiers"></a><a name="DelimitedIdentifiers"></a>分隔識別碼  
 分隔識別碼以方括號 ([ ]) 括住。  下列是包含符合這些規則之分隔識別碼的 DMX 陳述式範例。  
  
```  
SELECT * FROM [Marketing_Clusters].CONTENT;  
```  
  
 不符合一般識別碼格式規則的識別碼，一定要分隔。 下列是具有包含空格之分隔識別碼的 DMX 陳述式範例：  
  
```  
SELECT * FROM [Targeted Mailing].CONTENT;  
```  
  
 在下列情況下使用分隔識別碼：  
  
-   您使用保留字作為物件名稱或部份的物件名稱時。  
  
     建議您不要使用保留的關鍵字作為物件名稱。 您從舊版升級的資料庫 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可能包含識別碼，其中包含在舊版中不是保留的文字， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 但這是的保留字 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 您可以使用分隔識別碼參考這類物件，直到您能夠變更物件的名稱為止。  
  
-   您使用未列為合格識別碼的字元時。  
  
     在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中，您可以使用分隔識別碼裡目前字碼頁中的任何字元；不過，在物件名稱中任意使用特殊字元可能會導致 DMX 陳述式很難讀取與維護。  
  
### <a name="rules-for-delimited-identifiers"></a>分隔識別碼的規則  
 下列是分隔識別碼的格式規則：  
  
1.  分隔識別碼可以包含的字元數與一般識別碼一樣 (從 1 到 100 個字元，不包含分隔符號字元)。  
  
2.  識別碼的主體可以包含目前字碼頁中所使用之任何字元的組合，包括分隔符號字元本身。 如果識別碼本身的主體包含分隔字元，就需要特殊的處理：  
  
    -   如果識別碼的主體包含左方括號 ([)，則不需要其他處理。  
  
    -   如果識別碼的主體包含右方括號 (])，您必須指定兩個右方括號 (]]) 來表示字碼頁內的這個符號。  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>分隔含多個部份的識別碼  
 使用限定的物件名稱時，您可能必須分隔構成物件名稱的多個識別碼。 您必須個別分隔每個識別碼。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [&#40;DMX&#41; 語法元素的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
