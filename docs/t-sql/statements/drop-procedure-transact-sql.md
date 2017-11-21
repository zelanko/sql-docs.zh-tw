---
title: "DROP PROCEDURE (TRANSACT-SQL) |Microsoft 文件"
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
- DROP PROCEDURE
- DROP_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing stored procedures
- dropping procedure groups
- deleting stored procedures
- deleting procedure groups
- DROP PROCEDURE statement
- dropping stored procedures
- stored procedures [SQL Server], removing
- removing procedure groups
ms.assetid: 1c2d7235-7b9b-4336-8f17-429e7d82c2c3
caps.latest.revision: 51
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b386dfca28622eb95eec500d909aa7190d081493
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-procedure-transact-sql"></a>DROP PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中目前的資料庫移除一個或多個預存程序或程序群組。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP { PROC | PROCEDURE } [ IF EXISTS ] { [ schema_name. ] procedure } [ ,...n ]  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP { PROC | PROCEDURE } { [ schema_name. ] procedure_name }  
```  
  
## <a name="arguments"></a>引數  
 *如果存在*  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 只有當它已經存在有條件地卸除程序。  
  
 *schema_name*  
 程序所屬之結構描述的名稱。 不能指定伺服器名稱或資料庫名稱。  
  
 *程序*  
 要移除的預存程序或預存程序群組的名稱。 無法卸除編碼程序群組內的個別程序；會卸除整個程序群組。  
  
## <a name="best-practices"></a>最佳作法  
 在移除任何預存程序之前，請先檢查相依物件並對應地修改這些物件。 卸除預存程序可能在這些物件未更新的情況下，造成相依物件和指令碼失敗。 如需詳細資訊，請參閱[檢視預存程序的相依性](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
## <a name="metadata"></a>中繼資料  
 若要顯示現有程序的清單，請查詢**sys.objects**目錄檢視。 若要顯示程序定義，請查詢**sys.sql_modules**目錄檢視。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要**控制項**程序中，權限或**ALTER**權限的程序所屬的結構描述或成員資格**db_ddladmin**固定的伺服器角色.  
  
## <a name="examples"></a>範例  
 下列範例會移除目前資料庫中的 `dbo.uspMyProc` 預存程序。  
  
```  
DROP PROCEDURE dbo.uspMyProc;  
GO  
```  
  
 下列範例會移除目前資料庫中的數個預存程序。  
  
```  
DROP PROCEDURE dbo.uspGetSalesbyMonth, dbo.uspUpdateSalesQuotes, dbo.uspGetSalesByYear;  
```  
  
 下列範例會移除`dbo.uspMyProc`預存程序，如果它存在，但如果程序不存在，不會造成錯誤。 此語法中是新[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  
  
```  
DROP PROCEDURE IF EXISTS dbo.uspMyProc;  
GO  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [sys.objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [刪除預存程序](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)  
  
  



