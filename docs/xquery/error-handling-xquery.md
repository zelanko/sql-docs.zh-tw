---
title: "錯誤處理 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- static errors
- errors [XQuery]
- XQuery, error handling
- dynamic errors [XQuery]
ms.assetid: 7dee3c11-aea0-4d10-9126-d54db19448f2
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d4bb61baa736b9bc4554524ee366359e41741d4e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="error-handling-xquery"></a>錯誤處理 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  W3C 規格允許靜態或動態地引發類型錯誤，以及定義靜態、動態及類型錯誤。  
  
## <a name="compilation-and-error-handling"></a>編譯和錯誤處理  
 句法不正確的 Xquery 運算式及 XML DML 陳述式會傳回編譯錯誤。 編譯階段會檢查 XQuery 運算式及 DML 陳述式的靜態類型正確性，並針對具類型的 XML 的類型推斷來使用 XML 結構描述。 如果因為類型安全違規，而導致運算式在執行階段失敗，就會引發靜態類型錯誤。 靜態錯誤的範例包括：加入字串至整數，以及針對具類型的資料來查詢不存在的節點。  
  
 XQuery 執行階段錯誤會轉換成空的序列，這一點有違 W3C 標準。 依據引動過程內容，這些序列可能會以空的 XML 或 NULL 傳播至查詢結果。  
  
 雖然執行階段轉換錯誤會被轉換成空的序列，但明確地轉換為正確的類型可讓使用者解決靜態錯誤。  
  
## <a name="static-errors"></a>靜態錯誤  
 靜態錯誤是使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 錯誤機制傳回。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，會靜態地傳回 XQuery 類型錯誤。 如需詳細資訊，請參閱[XQuery 與靜態類型](../xquery/xquery-and-static-typing.md)。  
  
## <a name="dynamic-errors"></a>動態錯誤  
 在 XQuery 中，大部份動態錯誤會對應到空白時序 ("()")。 但是，有兩個例外狀況：XQuery 彙總函式中的溢位條件，以及 XML-DML 驗證錯誤。 請注意，大部份動態錯誤會對應到空白時序。 否則，利用 XML 索引的優點而執行的查詢可能會發生意外的錯誤。 因此，為了使執行有效率又不會產生意外的錯誤，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 會將動態錯誤對應到 ()。  
  
 因為 () 是對應到 False，所以在動態錯誤在述詞內發生的情況下，經常不會引發錯誤而未改變語意。 但是，在某些情況下，傳回 () 而非動態錯誤，可能會導致非預期的結果。 以下是說明此點的範例。  
  
### <a name="example-using-the-avg-function-with-a-string"></a>範例：搭配字串使用 avg() 函數  
 在下列範例中， [avg 函數](../xquery/aggregate-functions-avg.md)呼叫以計算三個值的平均值。 其中一個值是一個字串。 因為此例中的 XML 執行個體不具類型，所以其內含的所有資料都屬於不具類型的不可部份完成類型。 **Avg （)**函式的第一次會轉換這些值**xs: double**之前計算平均值。 不過，此值， `"Hello"`，無法轉換成**xs: double**並建立動態錯誤。 在此情況下，而不是傳回動態錯誤，轉型的`"Hello"`至**xs: double**會導致空的序列。 **Avg （)**函式會忽略此值，計算平均值的兩個值，然後傳回 150。  
  
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
 當您使用[無法運作](../xquery/functions-on-boolean-values-not-function.md)述詞，例如`/SomeNode[not(Expression)]`，而且運算式導致動態錯誤，空的序列將會傳回而非錯誤。 套用**not （)**空序列傳回 True，而非錯誤。  
  
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
 **Fn:error()**函式不支援。  
  
## <a name="see-also"></a>請參閱＜  
 [XQuery 語言參考 &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XQuery 基本概念](../xquery/xquery-basics.md)  
  
  
