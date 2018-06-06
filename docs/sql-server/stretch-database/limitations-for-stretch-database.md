---
title: Stretch Database 的限制 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, limitations
- Stretch Database, blocking issues
- limitations (Stretch Database)
- blocking issues (Stretch Database)
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5537ba71505cf14657e69f0e3ec5ccb8b125ebf3
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773134"
---
# <a name="limitations-for-stretch-database"></a>Stretch Database 的限制
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  了解已啟用 Stretch 之資料表的限制，以及目前讓您無法為資料表啟用 Stretch 的限制。  
  
##  <a name="Caveats"></a> 已啟用 Stretch 之資料表的限制  
  
已啟用 Stretch 的資料表具有下列限制。  
  
### <a name="constraints"></a>條件約束  
-   在包含已移轉資料的 Azure 資料表中，未強制執行 UNIQUE 條件約束和 PRIMARY KEY 條件約束的唯一性。  
  
### <a name="dml-operations"></a>DML 作業  
-   在已啟用 Stretch 的資料表中或包含已啟用 Stretch 之資料表的檢視中，您無法 UPDATE (更新) 或DELETE (刪除) 已移轉的資料列，或可進行移轉的資料列。  
  
-   您無法將資料列 INSERT (插入) 至連結伺服器上已啟用 Stretch 的資料表中。  
  
### <a name="indexes"></a>索引  
-   您無法為含有已啟用 Stretch 之資料表的檢視建立索引。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引的篩選不會傳播到遠端資料表。  
  
##  <a name="Limitations"></a> 目前讓您無法為資料表啟用 Stretch 的限制  
   
 下列項目目前讓您無法為資料表啟用 Stretch。  
  
 ### <a name="table-properties"></a>資料表屬性  
-   具有超過 1,023 個資料行或超過 998 個索引的資料表  
  
-   FileTable 或包含 FILESTREAM 資料的資料表  
  
-   所複寫或主動使用變更追蹤或變更資料擷取的資料表  
  
-   記憶體最佳化的資料表  
  
### <a name="data-types"></a>資料類型  
-   text、ntext 和 image  
  
-   TIMESTAMP  
  
-   sql_variant  
  
-   XML  
  
-   CLR 資料類型 (包括 geometry、geography、hierarchyid 和 CLR 使用者定義類型)  
  
 ### <a name="column-types"></a>資料行類型  
 -   COLUMN_SET  
  
-   計算資料行  
  
### <a name="constraints"></a>條件約束  
-   預設條件約束和檢查條件約束  
  
-   參考資料表的外部索引鍵條件約束。 在父子式關聯性 (例如，Order 和 Order_Detail) 中，您可以啟用子資料表 (Order_Detail) 而非父資料表 (Order) 的 Stretch。  
  
### <a name="indexes"></a>索引  
-   全文檢索索引  
  
-   XML 索引  
  
-   空間索引  
  
-   參考資料表的索引檢視表  
  
## <a name="see-also"></a>另請參閱  
 [執行 Stretch Database Advisor 以識別 Stretch Database 的資料庫和資料表](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [為資料表啟用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
