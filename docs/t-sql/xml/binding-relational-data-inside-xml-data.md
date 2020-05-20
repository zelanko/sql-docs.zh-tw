---
title: 在 XML 資料中繫結關聯式資料 | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9a2253165045d74f669c52d0247b716e5576e8b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68051327"
---
# <a name="binding-relational-data-inside-xml-data"></a>在 XML 資料中繫結關聯式資料
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  您可以針對 **xml** 資料類型變數或資料行指定 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)。 例如，[query&#40;&#41; 方法 &#40;xml 資料類型&#41;](../../t-sql/xml/query-method-xml-data-type.md) 會針對 XML 執行個體來執行所指定的 XQuery。 當您以這種方式來建構 XML 時，可能會想要引用非 XML 類型資料行或 Transact-SQL 變數中的值。 此程序就稱為：在 XML 資料中繫結關聯式資料。  
  
 為了在 XML 中繫結非 XML 的關聯式資料，SQL Server Database Engine 提供了下列虛擬函數：  
  
-   [sql:column&#40;&#41; 函數 &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-column.md) 可讓您在 XQuery 或 XML DML 運算式中使用關聯資料行的值。  
  
-   [sql:variable&#40;&#41; 函數 &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-variable.md) . 可讓您在 XQuery 或 XML DML 運算式中使用 SQL 變數的值。  
  
 每當您想要公開 XML 內的關聯值時，就可以搭配 **xml** 資料類型方法使用這些函數。  
  
 您不能使用這些函數來參考 **xml**、CLR 使用者定義型別、datetime、smalldatetime、**text**、**ntext**、**sql_variant** 和 **image** 類型之資料行或變數中的資料。  
  
 此外，這種繫結方式是唯讀的。 意即，您不能在使用這些函數的資料行中寫入資料。 例如，不允許下列語法：sql:variable("\@x")="某個運算式 *"* 。  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>範例：Cross-domain Query Using sql:variable()  
 此範例會示範 **sql:variable()** 如何讓應用程式將查詢參數化。 ISBN 的傳入方式是使用 SQL 變數 @isbn。 將常數置換成 **sql:variable()** 之後，就可以使用該查詢來搜尋任何 ISBN，而不只是 ISBN 為 0-7356-1588-2 的 ISBN。  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **sql:column()** 的用法類似，且提供更多的好處。 因為有以成本為考量的查詢最佳化工具，在資料行上使用索引會更有效率。 此外，計算資料行可能會儲存已升級的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  
