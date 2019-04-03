---
title: 在 OPENXML 中使用 value () 和 nodes () 方法 | Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- OpenXML method [XML in SQL Server]
- value method [XML in SQL Server]
- nodes method [XML in SQL Server]
ms.assetid: c73dbe55-d685-42eb-b0ee-9f3c5b9d97f3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4dabca94aba07a2d41a70bbee5343fe1eeb61658
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509895"
---
# <a name="use-the-value-and-nodes-methods-with-openxml"></a>在 OPENXML 中使用 value () 和 nodes () 方法
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  您可以在 **SELECT** 子句的 **xml** 資料類型上使用多重 **value()** 方法，以產生擷取值的資料列集。 **nodes()** 方法會針對可用於額外查詢的每個選定節點，各產生一個內部參考。 在產生資料列集時，如果所產生的資料列集會有數個資料行，且用來產生資料列集的路徑運算式很複雜時，合併 **nodes()** 和 **value()** 方法會比較有效率。  
  
 **nodes()** 方法會產生特殊 **xml** 資料類型的執行個體，其中每個執行個體都將其內容設定至不同的選取節點。 這種 XML 執行個體可支援 **query()**、**value()**、**nodes()** 和 **exist()** 方法，並可用於 **count(\*)** 彙總。 所有其他用法都會導致錯誤。  
  
## <a name="example-using-nodes"></a>範例使用 nodes()  
 假設您要擷取作者的姓名，而名字部份不是 "David"。 此外，您還想要將此資訊擷取成包含二個資料行 (FirstName 及 LastName) 的資料列集。 您可以使用 **nodes()** 和 **value()** 方法來完成此作業，如下所示：  
  
```  
SELECT nref.value('(first-name/text())[1]', 'nvarchar(50)') FirstName,  
       nref.value('(last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T CROSS APPLY xCol.nodes('//author') AS R(nref)  
WHERE  nref.exist('first-name[. != "David"]') = 1  
```  
  
 在此範例中， `nodes('//author')` 會產生參考各個 XML 執行個體之 `<author>` 元素的資料列集。 藉由評估與那些參考有關的 **value()** 方法，即可取得作者的姓名。  
  
 SQL Server 2000 提供一種功能，可使用 **OpenXml()** 從 XML 執行個體產生資料列集。 您可以指定資料列集的關聯式結構描述，以及 XML 執行個體中的值要如何對應到資料列集中的資料行。  
  
## <a name="example-using-openxml-on-the-xml-data-type"></a>範例在 xml 資料類型上使用 OpenXml()  
 您可以依下列方式使用 **OpenXml()** 來改寫上一個範例中的查詢。 這個方式是建立資料指標來將每個 XML 執行個體讀入 XML 變數，然後再套用 OpenXML：  
  
```  
DECLARE name_cursor CURSOR  
FOR  
   SELECT xCol   
   FROM   T  
OPEN name_cursor  
DECLARE @xmlVal XML  
DECLARE @idoc int  
FETCH NEXT FROM name_cursor INTO @xmlVal  
  
WHILE (@@FETCH_STATUS = 0)  
BEGIN  
   EXEC sp_xml_preparedocument @idoc OUTPUT, @xmlVal  
   SELECT   *  
   FROM   OPENXML (@idoc, '//author')  
          WITH (FirstName  varchar(50) 'first-name',  
                LastName   varchar(50) 'last-name') R  
   WHERE  R.FirstName != 'David'  
  
   EXEC sp_xml_removedocument @idoc  
   FETCH NEXT FROM name_cursor INTO @xmlVal  
END  
CLOSE name_cursor  
DEALLOCATE name_cursor   
```  
  
 **OpenXml()** 會建立一個 in-memory 表示法，並使用工作資料表來代替查詢處理器。 它是倚賴 MSXML 3.0 版的 XPath 1.0 版處理器，而不是 XQuery 引擎。 即使是在同一個 XML 執行個體上，工作資料表還是不能讓多個 **OpenXml()** 呼叫共用。 這限制了它的可調適性。 **OpenXml()** 可讓您在沒有指定 WITH 子句的情況下，存取 XML 資料的邊緣資料表格式。 此外，也可以讓您在另一個「溢位」資料行中使用其餘的 XML 值。  
  
 **nodes()** 與 **value()** 函數的組合可以有效地利用 XML 索引。 因此，這種組合所展現的可調適性比 **OpenXml**好。  
  
## <a name="see-also"></a>另請參閱  
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
