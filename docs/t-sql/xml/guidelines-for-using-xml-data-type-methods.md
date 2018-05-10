---
title: 使用 xml 資料類型方法的指導方針 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4ea4da8b314d5f7a55c8a3ca2a5913440f5c9268
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="guidelines-for-using-xml-data-type-methods"></a>使用 xml 資料類型方法的指導方針
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本主題將描述使用 **xml** 資料類型方法的指導方針。  
  
## <a name="the-print-statement"></a>PRINT 陳述式  
 **xml** 資料類型方法不能用於 PRINT 陳述式中，如下列範例所示。 **xml** 資料類型方法會被視為子查詢，而 PRINT 陳述式中不允許有子查詢。 因此，下列範例會傳回錯誤：  
  
```  
DECLARE @x xml  
SET @x = '<root>Hello</root>'  
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)   
```  
  
 解決方案是先將 **value()** 方法的結果指派到 **xml** 類型的變數中，然後再於查詢中指定變數。  
  
```  
DECLARE @x xml  
DECLARE @c varchar(max)  
SET @x = '<root>Hello</root>'  
SET @c = @x.value('/root[1]', 'varchar(11)')  
PRINT @c                                                        
```  
  
## <a name="the-group-by-clause"></a>GROUP BY 子句  
 **xml** 資料類型方法在內部會被視為子查詢。 因為 GROUP BY 需要純量，且不允許彙總及子查詢，所以您不能在 GROUP BY 子句中指定 **xml** 資料類型方法。 解決方案是，在其中呼叫使用 XML 方法的使用者自訂函數。  
  
## <a name="reporting-errors"></a>報告錯誤  
 報告錯誤時，**xml** 資料類型方法會以下列格式引發單一錯誤：  
  
```  
Msg errorNumber, Level levelNumber, State stateNumber:  
XQuery [database.table.method]: description_of_error  
```  
  
 例如：  
  
```  
Msg 2396, Level 16, State 1:  
XQuery [xmldb_test.xmlcol.query()]: Attribute may not appear outside of an element  
```  
  
## <a name="singleton-checks"></a>單一性檢查  
 如果編譯器無法判斷是否能在執行階段保證單一性，則需要單一性的尋找步驟、函數參數及運算子將會傳回錯誤。 這個問題經常發生在不具類型的資料上。 例如，查閱屬性時需要單一父元素。 選擇單一父節點的序數即已足夠。 評估 **node()**-**value()** 組合來擷取屬性值時，可能不需要指定序數。 下一個範例將會加以說明。  
  
### <a name="example-known-singleton"></a>範例：已知的單一性  
 在此範例中，**nodes()** 方法會針對每一個 <`book`> 元素各產生一個資料列。 在 <`book`> 節點上評估的 **value()** 方法會擷取 @genre 的值，而且作為一個屬性，它是單一的。  
  
```  
SELECT nref.value('@genre', 'varchar(max)') LastName  
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)  
```  
  
 XML 結構描述可用來檢查具類型之 XML 的類型。 如果在 XML 結構描述中將節點指定為單一性，編譯器就會使用該資訊，而且不會發生錯誤。 否則，就需要有選擇單一節點的序數。 尤其是，使用 descendant-or-self 座標軸 (//) (例如在 /book//title 中) 時，會放鬆 \<title> 元素的單一基數推斷，即使 XML 結構描述指定要如此。 因此，您應將它改寫成 (/book//title)[1]。  
  
 在執行類型檢查時，應隨時注意 //first-name[1] 與 (//first-name)[1] 之間的差異，這是很重要的。 前者會傳回 \<first-name> 節點的序列，其中每個節點都是同層級中最左邊的 \<first-name> 節點。 後者會傳回 XML 執行個體中，文件順序中的第一個單一 \<first-name> 節點。  
  
### <a name="example-using-value"></a>範例：使用 value()  
 下面這個在不具類型 XML 資料行上執行的查詢會導致靜態的編譯錯誤。這是因為 **value()** 預期以單一節點來作為第一個引數，而編譯器無法判斷在執行階段是否只會出現一個 \<last-name> 節點：  
  
```  
SELECT xCol.value('//author/last-name', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 您可以考慮下面這個解決方案：  
  
```  
SELECT xCol.value('//author/last-name[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 然而，這個解決方案並不能解決錯誤，因為每個 XML 執行個體中可能都會出現多個 <`author`> 節點。 下列改寫方案可以奏效：  
  
```  
SELECT xCol.value('(//author/last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 此查詢會傳回每個 XML 執行個體中第一個 `<last-name>` 元素的值。  
  
## <a name="see-also"></a>另請參閱  
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  
