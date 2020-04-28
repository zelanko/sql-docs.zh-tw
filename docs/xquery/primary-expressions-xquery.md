---
title: 主要運算式（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e3504b4f04b1b9842f786eeef3ecf1f105563f5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74200518"
---
# <a name="primary-expressions-xquery"></a>主要運算式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 主要運算式包含常值、變數參考、內容項目運算式、建構函式以及函數呼叫。  
  
## <a name="literals"></a>常值  
 XQuery 常式可為數值或字串常值。 字串常值可為包含預先定義的實體參考，而且實體參考是字元序列。 以連字號開始的序列代表單一字元，否則可能有語法意義。 以下是預先定義的 XQuery 實體參考。  
  
|實體參考|表示|  
|----------------------|----------------|  
|`&lt;`|\<|  
|`&gt;`|>|  
|`&amp;`|&|  
|`&quot;`|"|  
|`&apos;`|'|  
  
 字串常也可以包含字元參考、Unicode 字元的 XML 樣式參考，是由十進位或十六進位的字碼指標所識別。 例如，歐元符號可以用字元參考 "&\#8364;" 表示。  
  
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
SELECT @var.query(' <SalaryRange>Salary &gt; 50000 and &lt; 100000</SalaryRange>')  
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
  
 內建的布耳函數**true （）** 和**false （）** 可以用來代表布林值，如下列範例所示。  
  
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
DECLARE namespace x="https://X";  
for $x:i in /root return data($x:i)')  
GO  
```  
  
 您可以使用 sql： variable （）延伸函數來參考 SQL 變數，如下列查詢所示。  
  
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
  
-   不支援外部變數宣告。 此解決方案的解決方法是使用[sql： variable （）函數](../xquery/xquery-extension-functions-sql-variable.md)。  
  
## <a name="context-item-expressions"></a>內容項目運算式  
 內容項目是路徑運算式內容中目前所處理的項目。 會在具有文件節點的非 NULL XML 資料類型執行個體中初始化它。 它也可以在 XPath 運算式或 [] 述詞的內容中，由節點（）方法來變更。  
  
 內容項目是由包含點 (.) 的運算式所傳回的內容項目。 例如，下列查詢會評估屬性`a` `attr`是否存在 <> 的每個元素。 如果該屬性存在，就會傳回元素。 請注意，在述詞中的條件指定了單一句號所指定的內容節點。  
  
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
 您可以呼叫內建的 XQuery 函數和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sql： variable （）和 sql： column （）函數。 如需已實作用的函式清單，請參閱[針對 Xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)。  
  
#### <a name="implementation-limitations"></a>實作限制  
 以下為實作限制：  
  
-   不支援在 XQuery 初構中的函數宣告。  
  
-   不支援函數匯入。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;XQuery&#41;的 XML 結構](../xquery/xml-construction-xquery.md)
 
