---
title: 修改 XML 索引 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XML indexes [SQL Server], modifying
- modifying indexes
ms.assetid: 24d50fe1-c6ec-49e6-91a3-9791851ba53d
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 87e16b7c52a01b3755a5e7fb7d232f937470953c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="modify-xml-indexes"></a>修改 XML 索引
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 陳述式可用來修改現有的 XML 和非 XML 索引。 然而，並非所有的 ALTER INDEX 選項都可供 XML 索引使用。 在修改 XML 索引時，下列選項是無效的：  
  
-   重建和設定選項 IGNORE_DUP_KEY 對於 XML 索引是無效的。 對於次要 XML 索引，重建選項 ONLINE 必須設定為 OFF。 在 ALTER INDEX 陳述式中不允許使用 DROP_EXISTING 選項。  
  
-   在使用者資料表中對於主索引鍵條件約束的修改，並不會自動傳播至 XML 索引。 使用者必須先卸除 XML 索引，再重新建立它們。  
  
-   如果指定了 ALTER INDEX ALL，它會同時套用至非 XML 與 XML 索引。 索引選項可以指定為對於兩種索引類型都無效。 在此情況下，整個陳述式都會失敗。  
  
## <a name="example-modifying-an-xml-index"></a>範例：修改 XML 索引  
 下列範例會建立 XML 索引，然後將 `ALLOW_ROW_LOCKS` 選項設定為 `OFF`來加以修改。 當 `ALLOW_ROW_LOCKS` 為 `OFF`時，將不會鎖定資料列，並可使用頁面與資料表層級鎖定來取得指定索引的存取權。  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create primary XML index.   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
  
-- Modify and set an index option.  
ALTER INDEX PIdx_T_XmlCol on T   
SET (ALLOW_ROW_LOCKS = OFF)  
```  
  
## <a name="example-disabling-and-enabling-an-xml-index"></a>範例：停用和啟用 XML 索引  
 依預設，XML 索引為已啟用。 如果停用了 XML 索引，針對 XML 資料行執行的查詢將不會使用 XML 索引。 若要啟用 XML 索引，請使用 `ALTER INDEX` 搭配 `REBUILD` 選項。  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol ON T(XmlCol)  
GO  
ALTER INDEX PIdx_T_XmlCol on T DISABLE  
Go  
-- Verify index is disabled.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
-- Rebuild the index.  
ALTER INDEX PIdx_T_XmlCol on T REBUILD  
Go  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 索引 &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
