---
title: 錯誤處理（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- static errors
- errors [XQuery]
- XQuery, error handling
- dynamic errors [XQuery]
ms.assetid: 7dee3c11-aea0-4d10-9126-d54db19448f2
author: rothja
ms.author: jroth
ms.openlocfilehash: 1be899b95a4e132c3b5aa42a73df9bd1b0ee057c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68038960"
---
# <a name="error-handling-xquery"></a>錯誤處理 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  W3C 規格允許靜態或動態地引發類型錯誤，以及定義靜態、動態及類型錯誤。  
  
## <a name="compilation-and-error-handling"></a>編譯和錯誤處理  
 句法不正確的 Xquery 運算式及 XML DML 陳述式會傳回編譯錯誤。 編譯階段會檢查 XQuery 運算式及 DML 陳述式的靜態類型正確性，並針對具類型的 XML 的類型推斷來使用 XML 結構描述。 如果因為類型安全違規，而導致運算式在執行階段失敗，就會引發靜態類型錯誤。 靜態錯誤的範例包括：加入字串至整數，以及針對具類型的資料來查詢不存在的節點。  
  
 XQuery 執行階段錯誤會轉換成空的序列，這一點有違 W3C 標準。 依據引動過程內容，這些序列可能會以空的 XML 或 NULL 傳播至查詢結果。  
  
 雖然執行階段轉換錯誤會被轉換成空的序列，但明確地轉換為正確的類型可讓使用者解決靜態錯誤。  
  
## <a name="static-errors"></a>靜態錯誤  
 靜態錯誤是使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 錯誤機制傳回。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，會靜態地傳回 XQuery 類型錯誤。 如需詳細資訊，請參閱[XQuery 和靜態類型](../xquery/xquery-and-static-typing.md)。  
  
## <a name="dynamic-errors"></a>動態錯誤  
 在 XQuery 中，大部份動態錯誤會對應到空白時序 ("()")。 但是，有兩個例外狀況：XQuery 彙總函式中的溢位條件，以及 XML-DML 驗證錯誤。 請注意，大部份動態錯誤會對應到空白時序。 否則，利用 XML 索引的優點而執行的查詢可能會發生意外的錯誤。 因此，為了使執行有效率又不會產生意外的錯誤，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會將動態錯誤對應到 ()。  
  
 因為 () 是對應到 False，所以在動態錯誤在述詞內發生的情況下，經常不會引發錯誤而未改變語意。 但是，在某些情況下，傳回 () 而非動態錯誤，可能會導致非預期的結果。 以下是說明此點的範例。  
  
### <a name="example-using-the-avg-function-with-a-string"></a>範例：搭配字串使用 avg() 函數  
 在下列範例中，會呼叫[avg 函數](../xquery/aggregate-functions-avg.md)來計算三個值的平均值。 其中一個值是一個字串。 因為此例中的 XML 執行個體不具類型，所以其內含的所有資料都屬於不具類型的不可部份完成類型。 **Avg （）** 函數會先將這些值轉換為**xs： double** ，再計算平均值。 不過，值`"Hello"`無法轉換為**xs： double** ，而且會建立動態錯誤。 在此情況下，將轉換`"Hello"`成**xs： double** ，而不是傳回動態錯誤，會造成空的序列。 **Avg （）** 函數會忽略這個值、計算其他兩個值的平均值，然後傳回150。  
  
```  
DECLARE @x xml  
SET @x=N'<root xmlns:myNS="test">  
 <a>100</a>  
 <b>200</b>  
 <c>Hello</c>  
</root>'  
SELECT @x.query('avg(//*)')  
```  
  
### <a name="example-using-the-not-function"></a>範例：使用 not 函數  
 當您在述詞中使用[not 函數](../xquery/functions-on-boolean-values-not-function.md)時（例如， `/SomeNode[not(Expression)]`），而運算式會造成動態錯誤，則會傳回空的序列，而不是錯誤。 將**not （）** 套用至空的序列會傳回 True，而不是錯誤。  
  
### <a name="example-casting-a-string"></a>範例：轉換字串  
 在以下範例中，會將常值字串 "NaN" 轉換成 xs:string，然後再轉換成 xs:double。 結果會是一個空白資料列集。 雖然無法順利將字串 "NaN" 轉換成 xs:double，但是因為此字串會先轉換成 xs:string，所以此點要到執行階段才會確定。  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double(xs:string("NaN")) ')  
GO  
```  
  
 但是在此範例中，會發生靜態類型錯誤。  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double("NaN") ')  
GO  
```  
  
#### <a name="implementation-limitations"></a>實作限制  
 不支援**fn： error （）** 函數。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XQuery 基本概念](../xquery/xquery-basics.md)  
  
  
