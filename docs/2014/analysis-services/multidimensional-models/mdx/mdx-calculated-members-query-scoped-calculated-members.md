---
title: 建立查詢範圍匯出成員（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- query-scoped calculated members [MDX]
ms.assetid: c4507149-e67b-4e5d-9192-cc911acd9adc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e6153b78b0dda1a72e2f7dfd790fa8bcecd0bb37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074533"
---
# <a name="creating-query-scoped-calculated-members-mdx"></a>建立查詢範圍導出成員 (MDX)
  如果單一多維度運算式 (MDX) 查詢只需要有導出成員，您可以使用 WITH 關鍵字來定義導出成員。 查詢完成執行之後，使用 WITH 關鍵字建立的導出成員就不再存在。  
  
 如同本主題所討論，WITH 關鍵字的語法很有彈性，甚至允許導出成員以另一個導出成員為基底。  
  
> [!NOTE]  
>  如需建立導出成員的詳細資訊，請參閱[在 MDX 中建立導出成員 &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md)。  
  
## <a name="with-keyword-syntax"></a>WITH 關鍵字語法  
 使用以下語法將 WITH 關鍵字加入 MDX SELECT  陳述式：  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ] SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]FROM <SELECT subcube clause> [ <SELECT slicer axis clause> ][ <SELECT cell property list clause> ]  
<SELECT WITH clause> ::=  
   ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>) | <CREATE MEMBER body clause> ::= Member_Identifier AS 'MDX_Expression'  
   [ <CREATE MEMBER property clause> [ , <CREATE MEMBER property clause> ... ] ]  
<CREATE MEMBER property clause> ::=  
   ( MemberProperty_Identifier = Scalar_Expression )  
  
```  
  
 在 WITH 關鍵字的語法中， `Member_Identifier` 值是導出成員的完整名稱。 此完整名稱包括與導出成員相關的維度或層級。 
  `MDX_Expression` 值會在評估過運算式後，傳回導出成員的值。 導出成員的內建資料格屬性值也可以選擇性地藉由在 `MemberProperty_Identifier` 值中提供資料格屬性名稱，以及在 `Scalar_Expression` 值中提供資料格屬性的值來指定。  
  
## <a name="with-keyword-examples"></a>WITH 關鍵字範例  
 下列 MDX 查詢定義導出成員， `[Measures].[Special Discount]`，根據原始折扣量計算特殊折扣。  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 您也可以在階層內的任意點建立導出成員。 例如，下列 MDX 查詢定義假設之 Sales Cube 的 `[BigSeller]` 導出成員。 此導出成員可決定指定的商店是否至少賣出 100.00 單位的啤酒與葡萄酒。 但是，查詢建立的 `[BigSeller]` 導出成員不是 `[Product]` 維度的子成員，而是 `[Beer and Wine]` 成員的子成員。  
  
```  
WITH   
   MEMBER [Product].[Beer and Wine].[BigSeller] AS  
  IIf([Product].[Beer and Wine] > 100, "Yes","No")  
SELECT  
   {[Product].[BigSeller]} ON COLUMNS,  
   Store.[Store Name].Members ON ROWS  
FROM Sales  
  
```  
  
 導出成員不必只相依於 Cube 中的現有成員。 導出成員也能以相同 MDX 運算式中定義的其他導出成員為基底。 例如，以下 MDX 查詢使用第一個導出成員 `[Measures].[Special Discount]`中建立的值，來產生第二個導出成員 `[Measures].[Special Discounted Amount]`的值。  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Percentage] * 1.5,   
   FORMAT_STRING = 'Percent'  
  
   MEMBER [Measures].[Special Discounted Amount] AS  
   [Measures].[Reseller Average Unit Price] * [Measures].[Special Discount],   
   FORMAT_STRING = 'Currency'  
  
SELECT   
   {[Measures].[Special Discount], [Measures].[Special Discounted Amount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [SELECT 語句 &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [&#40;MDX&#41;建立會話範圍匯出成員](mdx-calculated-members-session-scoped-calculated-members.md)  
  
  
