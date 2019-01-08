---
title: sp_unprepare (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_unprepare_TSQL
- sp_cursor_unprepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unprepare
ms.assetid: 14320251-c551-49d8-b933-057406114978
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 54d615eb59fe3fd696cd125b3df15f29286d969d
ms.sourcegitcommit: f46fd79fd32a894c8174a5cb246d9d34db75e5df
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/26/2018
ms.locfileid: "53785799"
---
# <a name="spunprepare-transact-sql"></a>sp_unprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  捨棄 sp_prepare 預存程序所建立的執行計畫。 sp_unprepare 的叫用方式指定 ID = 15 中的表格式資料流 (TDS) 封包。  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_unprepare handle           
```  
  
## <a name="arguments"></a>引數  
 *控制代碼*  
 已*處理*sp_prepare 所傳回的值。  
  
## <a name="examples"></a>範例  
 下列範例會準備、執行及取消準備單一陳述式。  
  
```SQL  
DECLARE @P1 int;  
EXEC sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name = @P1 AND state_desc = @P2';  
EXEC sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會準備、執行及取消準備單一陳述式。  
  
```SQL  
DECLARE @P1 int;  
EXEC sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name = @P1 AND state_desc = @P2';  
EXEC sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   

