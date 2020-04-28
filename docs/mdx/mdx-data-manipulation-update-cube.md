---
title: UPDATE CUBE 語句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f52dd59b67b42ad430df9bb1e9d00dce7ad6d697
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68003525"
---
# <a name="mdx-data-manipulation---update-cube"></a>MDX 資料操作 - UPDATE CUBE


  UPDATE CUBE 陳述式可用來將資料寫回 Cube 中的任何資料格，再使用 SUM 彙總將其彙總至其父系。 如需更多說明和範例，請參閱此 blog 文章中的「瞭解配置」：[使用 Analysis Services 建立回寫應用程式（blog）](https://go.microsoft.com/fwlink/?LinkId=394977)。  
  
## <a name="syntax"></a>語法  
  
```  
  
UPDATE [ CUBE ] Cube_Name   
   SET   
            <update clause>   
           [, <update clause> ...n ]  
  
<update clause> ::=   
      Tuple_Expression[.VALUE]= New_Value  
      [   
        USE_EQUAL_ALLOCATION   
        | USE_EQUAL_INCREMENT   
        | USE_WEIGHTED_ALLOCATION [ BY Weight_Expression]   
        | USE_WEIGHTED_INCREMENT [ BY Weight_Expression]  
      ]  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 名稱的有效字串。  
  
 *Tuple_Expression*  
 傳回 Tuple 的有效多維度運算式 (MDX) 運算式。  
  
 *New_Value*  
 有效的數值運算式。  
  
 *Weight_Expression*  
 傳回介於 0 和 1 間之十進位值的有效多維度運算式 (MDX) 數值運算式。  
  
## <a name="remarks"></a>備註  
 您可以更新 Cube 內指定的分葉或非分葉資料格的值，選擇性地跨相依分葉資料格，配置指定的非分葉頁資料格的值。 由 Tuple 運算式指定的資料格可以是多維度空間的任何有效資料格 (亦即，資料格不需要是分葉資料格)。 不過，必須使用[Sum](../mdx/sum-mdx.md)彙總函式來匯總資料格，而且不能在用來識別資料格的元組中包含匯出成員。  
  
 將**UPDATE CUBE**語句視為副程式，將會自動產生一系列個別的資料格回寫作業到分葉和非分葉資料格，並將其匯總成指定的總和，這可能會很有説明。  
  
 以下是配置方法的描述。  
  
 **USE_EQUAL_ALLOCATION：** 提供給更新資料格的每個分葉資料格，將根據下列運算式指派一個相等的值。  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT：** 提供給更新資料格的每個分葉資料格都會根據下列運算式進行變更。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION：** 提供給更新資料格的每個分葉資料格，將會被指派一個以下列運算式為基礎的相等值。  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT：** 提供給更新資料格的每個分葉資料格都會根據下列運算式進行變更。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 如果未指定權數運算式， **UPDATE CUBE**語句會隱含地使用下列運算式。  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 加權運算式必須以零 (0) 到 1 之間的十進位值來表示。 這個值指定您要指派給受配置影響之分葉資料格的配置值比例。 用戶端應用程式設計人員負責建立的運算式，其積存彙總值將等於運算式配置值。  
  
> [!CAUTION]  
>  用戶端應用程式必須同時考慮所有維度的配置，避免發生非預期的結果，包括不正確的積存值或不一致的資料。  
  
 每個**更新 CUBE**配置都應該視為不可部分完成，以供交易之用。 這代表，如果有任何配置作業因任何原因而失敗，例如公式有誤，或安全性違規，整個 UPDATE CUBE 作業將會失敗。 處理個別配置作業之前，會先製作資料的快照集，以確定計算結果正確。  
  
> [!CAUTION]  
>  在包含整數的量值上使用時，累加的四捨五入變更會導致 USE_WEIGHTED_ALLOCATION 方法傳回不精確的結果。  
  
> [!IMPORTANT]  
>  當更新的資料格未重疊時， **Update Isolation Level** 連接字串屬性可用來增強 UPDATE CUBE 的效能。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Mdx&#41;&#40;mdx 資料動作陳述式](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
