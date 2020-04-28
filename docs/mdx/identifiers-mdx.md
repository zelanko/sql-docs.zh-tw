---
title: 識別碼（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c11561ac71aa72469a809ea25297d62133aa93da
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68891214"
---
# <a name="identifiers-mdx"></a>識別碼 (MDX)


  識別碼是 Analysis Services 物件的名稱。 每個物件都可以和都必須具有識別碼。 這包括 Cube、維度、階層、層級、成員等等。 您可以使用物件的識別碼，以參考多維度運算式 (MDX) 陳述式中的物件。  
  
 根據您如何命名物件，物件識別碼的識別碼將會是一般識別碼或是分隔識別碼。  
  
> [!NOTE]  
>  一般和分隔識別碼都必須包含1到100個字元。  
  
## <a name="using-regular-identifiers"></a>使用一般識別碼  
 一般識別碼是一個物件名稱，符合以下的一般識別碼格式化規則。 一般識別碼可以搭配或不搭配分隔符號來使用。  
  
### <a name="formatting-rules-for-regular-identifiers"></a>一般識別碼的格式化規則  
  
1.  第一個字元必須是以下任一項：  
  
    -   Unicode 標準2.0 所定義的字母。 除了其他語言的字母字元之外，字母的 Unicode 定義還包括從 a 到 z 與從 A 到 Z 的拉丁字元。  
  
    -   底線 (_)。  
  
2.  後續的字元可以是：  
  
    -   Unicode 標準2.0 中所定義的字母。  
  
    -   其他基本拉丁文或其他國家 (地區) 字集中的十進位數字。  
  
    -   底線 (_)。  
  
3.  識別碼絕不能是 MDX 保留關鍵字。 MDX 中的保留關鍵字不區分大小寫。 如需詳細資訊，請參閱[&#40;MDX 語法&#41;的保留關鍵字](../mdx/reserved-keywords-mdx-syntax.md)。  
  
4.  不允許內嵌的空格或特殊字元。  
  
### <a name="examples-of-regular-identifiers"></a>一般識別碼的範例  
 在以下 MDX 陳述式中，識別碼 `Measures`、`Product` 與 `Style` 符合一般識別碼的格式化規則。 這些一般識別碼不需要分隔符號。  
  
 `SELECT Measures.MEMBERS ON COLUMNS,`  
  
 `Product.Style.CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
 雖然不需要使用，但您還是可以將分隔符號與一般識別碼搭配使用。 在以下 MDX 陳述式中，已經使用方括號正確地分隔 `Measures`、`Product` 與 `Style` 一般識別碼。  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Product].[Style].CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
## <a name="using-delimited-identifiers"></a>使用分隔識別碼  
 不符合一般識別碼格式化規則的識別碼，一定要使用方括號 ([]) 分隔。  
  
> [!NOTE]  
>  分隔符號僅供識別使用。 不管 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中是否有關鍵字被標示為保留，關鍵字也不能使用分隔符號。  
  
 您可以在下列情況下使用分隔識別碼：  
  
-   當物件名稱或名稱的一部份使用保留關鍵字時。  
  
     建議您不要使用保留關鍵字作為物件名稱。 從舊版升級的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資料庫可能包含識別碼，其中包含舊版中未保留的字組，但現在已保留。 您可以使用分隔識別碼參考物件，直到您變更了物件的識別碼。  
  
-   當物件名稱使用未列為限定識別碼的字元時。  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 允許分隔識別碼使用目前字碼頁中的任何字元。 不過，於物件名稱任意使用特殊字元，會使 MDX 陳述式和指令碼難以讀懂和維護。  
  
### <a name="formatting-rules-for-delimited-identifiers"></a>分隔識別碼的格式化規則  
 分隔識別碼的主體可以包含目前字碼頁中的任何字元組合，包括分隔字元本身在內。 如果分隔識別碼的主體包含分隔字元，就需要特殊的處理：  
  
-   如果識別碼的主體只包含左方括號 ([)，則不需要其他處理。  
  
-   如果識別碼的主體包含右方括號 (])，您必須指定兩個右方括號 (]])。  
  
### <a name="examples-of-delimited-identifiers"></a>分隔識別碼的範例  
 在以下的假設 MDX 陳述式中，`Sales Volume`、`Sales Cube` 與 `select` 為分隔的識別碼：  
  
 `-- The [Sales Volume] and [Sales Cube] identifiers contain a space.`  
  
 `SELECT Measures.[Sales Volume]`  
  
 `FROM [Sales Cube]`  
  
 `WHERE Product.[select]`  
  
 `-- The [select] identifier is a reserved keyword.`  
  
 在下一個範例中，物件的名稱是 `Total Profit [Domestic]`。 若要參考此物件，您必須使用以下分隔識別碼：  
  
 `[Total Profit [Domestic]]]`  
  
 請注意，不需要變更 `Domestic` 前的左方括號，就可以建立分隔識別碼。 但是，必須以兩個右方括號取代 `Domestic` 後面的右方括號。  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>分隔含多個部份的識別碼  
 使用限定的物件名稱時，您可能必須分隔構成物件名稱的多個識別碼。 例如，需要分隔以下程式碼中的 Front Brakes 識別碼。  
  
 SELECT [Measures].MEMBERS ON COLUMNS,  
  
 [Product].[Product].[Front Brakes] ON ROWS  
  
 FROM [Adventure Works]  
  
 此外，前例中的 Measures 識別碼已經進行分隔，以示範如何分隔多個識別碼。  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 語言參考 &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)   
 [MDX 查詢基本概念 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services)   
 [MDX 語法元素 &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
