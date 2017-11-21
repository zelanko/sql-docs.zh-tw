---
title: "卸除結構描述 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SCHEMA
- DROP_SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting schemas
- schemas [SQL Server], removing
- DROP SCHEMA statement
- dropping schemas
- removing schemas
ms.assetid: 874aa29e-c8ad-41e4-a672-900fdc58f1f6
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 584aea443e3263f44367ede24d7a59b8564e92c1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-schema-transact-sql"></a>DROP SCHEMA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  從資料庫中移除結構描述。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP SCHEMA  [ IF EXISTS ] schema_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP SCHEMA schema_name  
```  
  
## <a name="arguments"></a>引數  
 *如果存在*  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 只有當它已經存在有條件地卸除結構描述。  
  
 *schema_name*  
 這是資料庫中結構描述的識別名稱。  
  
## <a name="remarks"></a>備註  
 要卸除的結構描述不能包含任何物件。 如果該結構描述包含物件，DROP 陳述式會失敗。  
  
 結構描述的相關資訊會顯示在[sys.schemas](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)目錄檢視。  
  
 **注意：**[!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 CONTROL 權限或資料庫的 ALTER ANY SCHEMA 權限。  
  
## <a name="examples"></a>範例  
 下列範例是從單一 `CREATE SCHEMA` 陳述式開始。 這個陳述式會建立結構描述 `Sprockets` (由 `Krishna` 擁有) 和資料表 `Sprockets.NineProngs`，然後將 `SELECT` 權限授與 `Anibal`，並拒絕將 `SELECT` 權限授與 `Hung-Fu`。  
  
```  
CREATE SCHEMA Sprockets AUTHORIZATION Krishna   
    CREATE TABLE NineProngs (source int, cost int, partnumber int)  
    GRANT SELECT TO Anibal   
    DENY SELECT TO Hung-Fu;  
GO  
```  
  
 下列陳述式會卸除該結構描述。 請注意，您必須先卸除該結構描述包含的資料表。  
  
```  
DROP TABLE Sprockets.NineProngs;  
DROP SCHEMA Sprockets;  
GO  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [建立結構描述 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [ALTER SCHEMA &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [卸除結構描述 (TRANSACT-SQL)](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  

