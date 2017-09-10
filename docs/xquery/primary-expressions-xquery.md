---
title: "主要運算式 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- variable references [XQuery]
- primary expressions [XQuery]
- function calls [XQuery]
- expressions [XQuery], primary
- literals [XQuery]
- context item expressions [XQuery]
ms.assetid: d4183c3e-12b5-4ca0-8413-edb0230cb159
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4340836259f69bfd723b8b1482f6d81c4198442c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="primary-expressions-xquery"></a>主要運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 主要運算式包含常值、變數參考、內容項目運算式、建構函式以及函數呼叫。  
  
## <a name="literals"></a>常值  
 XQuery 常式可為數值或字串常值。 字串常值可為包含預先定義的實體參考，而且實體參考是字元序列。 以連字號開始的序列代表單一字元，否則可能有語法意義。 以下是預先定義的 XQuery 實體參考。  
  
|實體參考|表示|  
|----------------------|----------------|  
|&lt;|\<|  
|&gt;|>|  
|&amp;|&|  
|&quot;|"|  
|&apos;|'|  
  
 字串常也可以包含字元參考、Unicode 字元的 XML 樣式參考，是由十進位或十六進位的字碼指標所識別。 歐元符號，例如由字元參考 」 （& s)\#8364;"。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用 XML 1.0 版做為剖析的基礎。  
  
### <a name="examples"></a>範例  
 下列範例說明常值的用途以及實體與字元的參考。  
  
 此程式碼傳回錯誤，因為 `<'` 和 `'>` 字元具有特殊意義。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 如果您改用實體參考，查詢即可執行成功。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 下列範例說明使用字元參考代表歐元符號。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <a>€12.50</a>')  
```  
  
 以下是結果。  
  
 `<a>€12.50</a>`  
  
 在下列範例中，查詢是以撇號分隔。 因此，在字串值中的撇號是由兩個相鄰撇號所代表。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>I don''t know</a>')  
Go  
```  
  
 以下是結果。  
  
 `<a>I don't know</a>`  
  
 內建布林函數， **true （)**和**false （)**，可用來代表布林值，如下列範例所示。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>{true()}</a>')  
GO  
```  
  
 直接的元素建構函式是以大括號指定運算式。 在產生的 XML 中，其值將會取代運算式。  
  
 以下是結果。  
  
 `<a>true</a>`  
  
## <a name="variable-references"></a>變數參考  
 在 XQuery 中的變數參考是在 QName 前面加上 $ 符號。 此實作僅支援未加前置詞的變數參考。 例如，下列查詢會在 FLWOR 運算式中定義變數 `$i`。  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
 for $i in /root return data($i)')  
GO  
```  
  
 下列查詢將無法成功執行，因為在變數名稱中加入了命名空間前置詞。  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
DECLARE namespace x="http://X";  
for $x:i in /root return data($x:i)')  
GO  
```  
  
 下列查詢中所示，您可以使用： variable （） 延伸模組函數參考 SQL 變數。  
  
```  
DECLARE @price money  
SET @price=2500  
DECLARE @x xml  
SET @x = ''  
SELECT @x.query('<value>{sql:variable("@price") }</value>')  
```  
  
 以下是結果。  
  
 `<value>2500</value>`  
  
#### <a name="implementation-limitations"></a>實作限制  
 以下為實作限制：  
  
-   不支援具有命名空間前置詞的變數。  
  
-   不支援模組匯入。  
  
-   不支援外部變數宣告。 對此的解決方案是使用[: variable （） 函式](../xquery/xquery-extension-functions-sql-variable.md)。  
  
## <a name="context-item-expressions"></a>內容項目運算式  
 內容項目是路徑運算式內容中目前所處理的項目。 會在具有文件節點的非 NULL XML 資料類型執行個體中初始化它。 它也可使用 nodes （） 方法，XPath 運算式的內容或 [] 述詞中變更。  
  
 內容項目是由包含點 (.) 的運算式所傳回的內容項目。 例如，下列查詢會評估每個元素 <`a`>，是否存在 `attr` 屬性。 如果該屬性存在，就會傳回元素。 請注意，在述詞中的條件指定了單一句號所指定的內容節點。  
  
```  
DECLARE @var XML  
SET @var = '<ROOT>  
<a>1</a>  
<a attr="1">2</a>  
</ROOT>'  
SELECT @var.query('/ROOT[1]/a[./@attr]')  
```  
  
 以下是結果。  
  
 `<a attr="1">2</a>`  
  
## <a name="function-calls"></a>函數呼叫  
 您可以呼叫內建 XQuery 函數和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]: variable （） 和： column （） 函式。 如需實作的函式的清單，請參閱[針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)。  
  
#### <a name="implementation-limitations"></a>實作限制  
 以下為實作限制：  
  
-   不支援在 XQuery 初構中的函數宣告。  
  
-   不支援函數匯入。  
  
## <a name="see-also"></a>另請參閱  
 [XML 建構 &#40;XQuery &#41;](../xquery/xml-construction-xquery.md)  
  
  
