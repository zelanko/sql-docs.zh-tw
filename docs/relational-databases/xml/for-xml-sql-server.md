---
title: FOR XML (SQL Server) | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, about FOR XML clause
- PATH FOR XML mode, construction
- EXPLICIT FOR XML mode
- RAW FOR XML mode
- retrieving XML data
- XML [SQL Server], FOR XML clause
- AUTO FOR XML mode
- XML [SQL Server], construction
ms.assetid: 2b6b5c61-c5bd-49d2-8c0c-b7cf15857906
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: 5d497064378b7fe34c95ffe9c886144bb3523256
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "67943337"
---
# <a name="for-xml-sql-server"></a>FOR XML (SQL Server)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

SELECT 查詢會將結果以資料列集的形式傳回。 在查詢中指定 FOR XML 子句，您就可選擇以 XML 格式擷取 SQL 查詢的正式結果。 FOR XML 子句可以在最上層的查詢與子查詢中使用。 最上層的 FOR XML 子句只能用在 SELECT 陳述式中。 在子查詢中，FOR XML 可以在 INSERT、UPDATE 與 DELETE 陳述式中使用。 FOR XML 也可以用在指派陳述式中。

在 FOR XML 子句中，您可以指定下列其中一個模式：

- RAW
- AUTO
- EXPLICIT
- PATH

RAW 模式會對資料列集中 SELECT 陳述式傳回的每一個資料列，產生一個 \<資料列> 項目。 您可以撰寫巢狀 FOR XML 查詢來產生 XML 階層。

AUTO 模式會使用啟發學習法 (根據 SELECT 陳述式的指定方式)，在所產生的 XML 中產生巢狀結構。 您對產生的 XML 之外觀只有最少的控制權。 您可以撰寫巢狀的 FOR XML 查詢，以產生 AUTO 模式啟發學習法所產生之 XML 外觀以外的 XML 階層。

EXPLICIT 模式可讓您對 XML 外觀有更多的控制權。 您在決定 XML 的外觀時，可依照意願混合屬性和元素。 因為查詢執行的關係，產生的結果資料列集需要有特定格式。 這個資料列集格式之後會對應到 XML 外觀。 EXPLICIT 模式的功能是可依照意願混合屬性和元素、建立包裝函數和巢狀的複雜屬性，以及建立以空格分隔的值 (例如，OrderID 屬性可能有順序識別碼值的清單) 和混合的內容。

不過，撰寫 EXPLICIT 模式的查詢比較繁雜。 您可以使用部份新的 FOR XML 功能，例如撰寫巢狀的 FOR XML RAW/AUTO/PATH 模式查詢和 TYPE 指示詞，而不要使用 EXPLICIT 模式來產生階層。 巢狀的 FOR XML 查詢可以產生您使用 EXPLICIT 模式可產生的任何 XML。 如需詳細資訊，請參閱 [使用巢狀 FOR XML 查詢](../../relational-databases/xml/use-nested-for-xml-queries.md) 和 [在 FOR XML 查詢中的 TYPE 指示詞](../../relational-databases/xml/type-directive-in-for-xml-queries.md)。

若搭配使用 PATH 模式和巢狀的 FOR XML 查詢功能，則能夠以較簡易的方式提供 EXPLICIT 模式的彈性。

只有在執行設定為這些模式的查詢時，這些模式才有效。 它們並不會影響任何後續查詢的結果。

對於任何搭配 FOR BROWSE 子句使用的選取項目而言，FOR XML 都是無效的。

## <a name="example"></a>範例

下列 `SELECT` 陳述式可從 `Sales.Customer` 資料庫的 `Sales.SalesOrderHeader` 與 `AdventureWorks2012` 資料表擷取資訊。 此查詢在 `AUTO` 子句中指定了 `FOR XML` 模式：

```sql
USE AdventureWorks2012
GO
SELECT Cust.CustomerID,
       OrderHeader.CustomerID,
       OrderHeader.SalesOrderID,
       OrderHeader.Status
FROM Sales.Customer Cust 
INNER JOIN Sales.SalesOrderHeader OrderHeader
ON Cust.CustomerID = OrderHeader.CustomerID
FOR XML AUTO;
```

## <a name="the-for-xml-clause-and-server-names"></a>FOR XML 子句和伺服器名稱

當包含 FOR XML 子句的 SELECT 陳述式在查詢中指定四部分的名稱時，若在本機電腦上執行查詢，則伺服器名稱並不會在產生的 XML 文件中傳回。 但如果是在網路伺服器上執行查詢，則伺服器名稱會以四個部分的名稱形式傳回。

例如，請考量以下的查詢：

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person
  FOR XML AUTO;
```

&nbsp;

**本機伺服器**：&nbsp; 若 `ServerName` 是本機伺服器，查詢會傳回下列文字：

```xml
<AdventureWorks2012.Person.Person LastName="Achong" />  
```

&nbsp;

**網路伺服器**：&nbsp; 若 `ServerName` 是網路伺服器，查詢將會傳回下列文字：

```xml
<ServerName.AdventureWorks2012.Person.Person LastName="Achong" />
```

&nbsp;

**避免模稜兩可**：&nbsp; 您可以指定下列別名來避免這種模稜兩可的情況：

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person x
  FOR XML AUTO;
```

現在，消除模稜兩可的查詢會傳回下列文字：

```xml
<x LastName="Achong"/>
```

## <a name="see-also"></a>另請參閱

[FOR XML 子句的基本語法](../../relational-databases/xml/basic-syntax-of-the-for-xml-clause.md)  
[搭配 FOR XML 使用 RAW 模式](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
[搭配 FOR XML 使用 AUTO 模式](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
[搭配 FOR XML 使用 EXPLICIT 模式](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
[搭配 FOR XML 使用 PATH 模式](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
[OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
[使用 WITH XMLNAMESPACES 將命名空間加入至查詢](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)
