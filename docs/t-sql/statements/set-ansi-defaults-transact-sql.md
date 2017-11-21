---
title: "SET ANSI_DEFAULTS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET ANSI_DEFAULTS
- ANSI_DEFAULTS
- SET_ANSI_DEFAULTS_TSQL
- ANSI_DEFAULTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ANSI_DEFAULTS option
- SET ANSI_DEFAULTS statement
ms.assetid: bd721d97-6e23-488b-8c8c-c0453d5b3b86
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 170fb1f5a95b9f6fe4fbe596906595475175b1a2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansidefaults-transact-sql"></a>SET ANSI_DEFAULTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  控制一群共同指定某些 ISO 標準行為的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_DEFAULTS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_DEFAULTS ON;  
```  
  
## <a name="remarks"></a>備註  
 SET ANSI_DEFAULTS 是用戶端不會修改的伺服器端設定。 用戶端會管理自己的設定。 依預設，這些設定與伺服器設定相反。 使用者不應該修改伺服器設定。 若要變更用戶端行為，使用者應使用 SQL_COPT_SS_PRESERVE_CURSORS。 如需詳細資訊，請參閱[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
 當啟用 (ON) 時，這個選項會啟用下列 ISO 設定：  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_NULL_DFLT_ON|SET IMPLICIT_TRANSACTIONS|  
|SET ANSI_PADDING|SET QUOTED_IDENTIFIER|  
|SET ANSI_WARNINGS||  
  
 這些 ISO 標準 SET 選項共同定義了使用者、執行中的觸發程序或預存程序之工作階段持續期間的查詢處理環境。 不過，這些 SET 選項並未包括符合 ISO 標準所需要的所有選項。  
  
 當處理計算資料行索引和索引檢視時，這些預設值其中的四個 (ANSI_NULLS、ANSI_PADDING、ANSI_WARNINGS 和 QUOTED_IDENTIFIER) 必須設為 ON。 這些預設值是在建立和變更計算資料行索引和索引檢視時，必須指派必要值的七個選項之中。 其他 SET 選項有 ARITHABORT (ON)、CONCAT_NULL_YIELDS_NULL (ON) 和 NUMERIC_ROUNDABORT (OFF)。 計算資料行上使用索引檢視表和索引所需的 SET 選項設定的相關資訊，請參閱"考量當您使用 SET 陳述式 」，在[SET 陳述式 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自動將 ANSI_DEFAULTS 設為 ON，連接時。 之後，驅動程式和提供者便將 CURSOR_CLOSE_ON_COMMIT 和 IMPLICIT_TRANSACTIONS 設為 OFF。 您可以在 ODBC 資料來源、ODBC 連接屬性中設定 SET CURSOR_CLOSE_ON_COMMIT 和 SET IMPLICIT_TRANSACTIONS 的 OFF 設定，或在應用程式連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前所設定的 OLE DB 連接屬性中設定這項設定。 起始於 DB-Library 應用程式的連接之 SET ANSI_DEFAULTS 預設值是 OFF。  
  
 當發出 SET ANSI_DEFAULTS 時，會在剖析階段設定 SET QUOTED_IDENTIFIER，執行階段所設定的選項如下：  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET ANSI_WARNINGS|  
|SET ANSI_NULL_DFLT_ON|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_PADDING|SET IMPLICIT_TRANSACTIONS|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會設定 `SET ANSI_DEFAULTS ON` 以及利用 `DBCC USEROPTIONS` 陳述式來顯示受影響的設定。  
  
```  
-- SET ANSI_DEFAULTS ON.  
SET ANSI_DEFAULTS ON;  
GO  
-- Display the current settings.  
DBCC USEROPTIONS;  
GO  
-- SET ANSI_DEFAULTS OFF.  
SET ANSI_DEFAULTS OFF;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DBCC USEROPTIONS &#40;TRANSACT-SQL &#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CURSOR_CLOSE_ON_COMMIT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET IMPLICIT_TRANSACTIONS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  

