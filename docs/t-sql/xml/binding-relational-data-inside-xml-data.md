---
title: "在 XML 資料的關聯式資料繫結 |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87dca9b5bcd70335a6121b1be1e49f4cc352826e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="binding-relational-data-inside-xml-data"></a>在 XML 資料中繫結關聯式資料
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  您可以指定[xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)針對**xml**資料類型變數或資料行。 例如，[查詢 &#40; &#41;方法 &#40; xml 資料類型 &#41;](../../t-sql/xml/query-method-xml-data-type.md)會針對 XML 執行個體指定的 XQuery。 當您以這種方式來建構 XML 時，可能會想要引用非 XML 類型資料行或 Transact-SQL 變數中的值。 此程序就稱為：在 XML 資料中繫結關聯式資料。  
  
 為了在 XML 中繫結非 XML 的關聯式資料，SQL Server Database Engine 提供了下列虛擬函數：  
  
-   [sql: column &#40; &#41;函式 &#40;XQuery &#41;](../../xquery/xquery-extension-functions-sql-column.md)可讓您在 XQuery 或 XML DML 運算式中使用關聯式資料行的值。  
  
-   [sql: variable &#40; &#41;函式 &#40;XQuery &#41;](../../xquery/xquery-extension-functions-sql-variable.md) . 可讓您在 XQuery 或 XML DML 運算式中使用 SQL 變數的值。  
  
 您可以使用這些函式**xml**資料類型方法，每當您想要公開 XML 內的關聯式值。  
  
 您無法使用這些函式來參考資料行或變數中的資料**xml**，CLR 使用者定義類型、 datetime、 smalldatetime、**文字**， **ntext**， **sql_variant**，和**映像**型別。  
  
 此外，這種繫結方式是唯讀的。 意即，您不能在使用這些函數的資料行中寫入資料。 例如，sql:variable("@x") ="*某些運算式"*不允許。  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>範例：Cross-domain Query Using sql:variable()  
 這個範例會示範如何**: variable （)**可以讓應用程式將查詢參數化。 ISBN 的傳入方式使用 SQL 變數@isbn。 取代具有常數**: variable （)**，查詢可以用來搜尋任何 ISBN，而不只是 ISBN 為 0-7356-1588年-2 的一個。  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **: column （)**可以用類似的方式，並提供額外的好處。 因為有以成本為考量的查詢最佳化工具，在資料行上使用索引會更有效率。 此外，計算資料行可能會儲存已升級的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  
