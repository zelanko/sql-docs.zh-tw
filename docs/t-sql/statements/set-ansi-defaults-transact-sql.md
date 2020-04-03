---
title: SET ANSI_DEFAULTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9fa8bd2c029ea65bb03e21543212dd11b65f2242
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "80345461"
---
# <a name="set-ansi_defaults-transact-sql"></a>SET ANSI_DEFAULTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  控制一群共同指定某些 ISO 標準行為的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>語法

```
-- Syntax for SQL Server

SET ANSI_DEFAULTS { ON | OFF }
```

```
-- Syntax for Azure Synapse and Parallel Data Warehouse

SET ANSI_DEFAULTS ON
```

## <a name="remarks"></a>備註  
ANSI_DEFAULTS 是可啟用所有用戶端連線行為的伺服器端設定。 用戶端通常會要求對連線或工作階段初始化進行設定。 使用者不應該修改伺服器設定。   
若要變更用戶端行為，使用者應使用用戶端特定方法，例如 `SQL_COPT_SS_PRESERVE_CURSORS`。 如需詳細資訊，請參閱 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。
  
當啟用 (ON) 時，這個選項會啟用下列 ISO 設定：  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_NULL_DFLT_ON|SET IMPLICIT_TRANSACTIONS|  
|SET ANSI_PADDING|SET QUOTED_IDENTIFIER|  
|SET ANSI_WARNINGS||  
  
這些 ISO 標準 SET 選項共同定義了使用者、執行中的觸發程序或預存程序之工作階段持續期間的查詢處理環境。 不過，這些 SET 選項並未包括符合 ISO 標準所需要的所有選項。  
  
當處理計算資料行索引和索引檢視表時，這些預設值其中的四個 (`ANSI_NULLS`、`ANSI_PADDING`、`ANSI_WARNINGS` 和 `QUOTED_IDENTIFIER`) 必須設為 ON。 這些預設值是在建立和變更計算資料行索引和索引檢視時，必須指派必要值的七個選項之中。 其他 SET 選項包括 `ARITHABORT` (ON)、`CONCAT_NULL_YIELDS_NULL` (ON) 和 `NUMERIC_ROUNDABORT` (OFF)。 如需有關含索引檢視表和計算資料行索引之必要 SET 選項設定的詳細資訊，請參閱[SET 陳述式的使用考量](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements)。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者在連接時，都會自動將 ANSI_DEFAULTS 設為 ON。 之後，驅動程式和提供者便將 CURSOR_CLOSE_ON_COMMIT 和 IMPLICIT_TRANSACTIONS 設為 OFF。 您可在 ODBC 資料來源、ODBC 連線屬性或 OLE DB 連線屬性中設定 `CURSOR_CLOSE_ON_COMMIT` 和 `IMPLICIT_TRANSACTIONS` 的 OFF 設定，再連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 就來自 DB-Library 應用程式的連線而言，`ANSI_DEFAULTS` 的預設值是 OFF。  
  
當發出 SET ANSI_DEFAULTS 時，會在剖析階段設定 QUOTED_IDENTIFIER，而在執行階段則會設定下列選項：  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET ANSI_WARNINGS|  
|SET ANSI_NULL_DFLT_ON|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_PADDING|SET IMPLICIT_TRANSACTIONS|  
  
## <a name="permissions"></a>權限  
需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
下列範例會將 ANSI_DEFAULTS 設定為 ON，並使用 `DBCC USEROPTIONS` 陳述式來顯示受影響的設定。  
  
```sql  
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
 [DBCC USEROPTIONS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
