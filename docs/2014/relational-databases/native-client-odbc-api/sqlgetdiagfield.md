---
title: SQLGetDiagField |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetDiagField function
ms.assetid: 395245ba-0372-43ec-b9a4-a29410d85a6d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fb158b2c11f48733c5eacb3827a43a3303c4a51
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62657701"
---
# <a name="sqlgetdiagfield"></a>SQLGetDiagField
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式會針對`SQLGetDiagField`指定下列額外的診斷欄位。 這些欄位支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應用程式的豐富錯誤報告功能，並且可用於在連接的 ODBC 連接控制代碼和 ODBC 陳述式控制代碼上產生的所有診斷記錄。 欄位會定義在 sqlncli.h 中。  
  
|診斷記錄欄位|描述|  
|------------------------------|-----------------|  
|SQL_DIAG_SS_LINE|報告產生錯誤的預存程序的行號。 SQL_DIAG_SS_LINE 的值只有在 SQL_DIAG_SS_PROCNAME 傳回值時才有意義。 值會以不帶正負號的 16 位元整數傳回。|  
|SQL_DIAG_SS_MSGSTATE|錯誤訊息的狀態。 如需錯誤訊息狀態的詳細資訊，請參閱[RAISERROR](/sql/t-sql/language-elements/raiserror-transact-sql)。 值會以帶正負號的 32 位元整數傳回。|  
|SQL_DIAG_SS_PROCNAME|產生錯誤的預存程序的名稱 (如果適用)。 值會以字元字串傳回。 字串的長度 (以字元為單位) 是依 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本而定， 您可以藉由呼叫[SQLGetInfo](sqlgetinfo.md)來要求 SQL_MAX_PROCEDURE_NAME_LEN 的值來判斷它。|  
|SQL_DIAG_SS_SEVERITY|相關錯誤訊息的嚴重性層級。 值會以帶正負號的 32 位元整數傳回。|  
|SQL_DIAG_SS_SRVNAME|錯誤發生所在之伺服器的名稱。 值會以字元字串傳回。 字串長度 (以字元表示) 是由 SQL_MAX_SQLSERVERNAME 巨集在 sqlncli.h 中定義。|  
  
 包含字元資料、SQL_DIAG_SS_PROCNAME 和 SQL_DIAG_SS_SRVNAME 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定診斷欄位，會將該資料以 ANSI、Unicode 或以 Null 結束的字元傳回給用戶端。 如有必要，字元計數可依字元寬度進行調整。 或者，TCHAR 或 SQLTCHAR 之類的可攜式 C 資料類型可用來確保正確的程式變數長度。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會支援下列其他的動態函數程式碼，以識別最後所嘗試的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式。 動態函數程式碼會以診斷記錄集的標頭 (記錄 0) 傳回，因此會在每次執行時使用 (不論成功與否)。  
  
|動態函數程式碼|來源|  
|---------------------------|------------|  
|SQL_DIAG_DFC_SS_ALTER_DATABASE|ALTER DATABASE 陳述式|  
|SQL_DIAG_DFC_SS_CHECKPOINT|CHECKPOINT 陳述式|  
|SQL_DIAG_DFC_SS_CONDITION|錯誤會發生在陳述式的 WHERE 或 HAVING 子句中。|  
|SQL_DIAG_DFC_SS_CREATE_DATABASE|CREATE DATABASE 陳述式|  
|SQL_DIAG_DFC_SS_CREATE_DEFAULT|CREATE DEFAULT 陳述式|  
|SQL_DIAG_DFC_SS_CREATE_PROCEDURE|CREATE PROCEDURE 陳述式|  
|SQL_DIAG_DFC_SS_CREATE_RULE|CREATE RULE 陳述式|  
|SQL_DIAG_DFC_SS_CREATE_TRIGGER|CREATE TRIGGER 陳述式|  
|SQL_DIAG_DFC_SS_CURSOR_DECLARE|DECLARE CURSOR 陳述式|  
|SQL_DIAG_DFC_SS_CURSOR_OPEN|OPEN 陳述式|  
|SQL_DIAG_DFC_SS_CURSOR_FETCH|FETCH 陳述式|  
|SQL_DIAG_DFC_SS_CURSOR_CLOSE|CLOSE 陳述式|  
|SQL_DIAG_DFC_SS_DEALLOCATE_CURSOR|DEALLOCATE 陳述式|  
|SQL_DIAG_DFC_SS_DBCC|DBCC 陳述式|  
|SQL_DIAG_DFC_SS_DENY|DENY 陳述式|  
|SQL_DIAG_DFC_SS_DROP_DATABASE|DROP DATABASE 陳述式|  
|SQL_DIAG_DFC_SS_DROP_DEFAULT|DROP DEFAULT 陳述式|  
|SQL_DIAG_DFC_SS_DROP_PROCEDURE|DROP PROCEDURE 陳述式|  
|SQL_DIAG_DFC_SS_DROP_RULE|DROP RULE 陳述式|  
|SQL_DIAG_DFC_SS_DROP_TRIGGER|DROP TRIGGER 陳述式|  
|SQL_DIAG_DFC_SS_DUMP_DATABASE|BACKUP 或 DUMP DATABASE 陳述式|  
|SQL_DIAG_DFC_SS_DUMP_TABLE|DUMP TABLE 陳述式|  
|SQL_DIAG_DFC_SS_DUMP_TRANSACTION|BACKUP 或 DUMP TRANSACTION 陳述式。 如果**chkpt 上的 trunc** ，也會針對 CHECKPOINT 語句傳回。 資料庫選項為 on。|  
|SQL_DIAG_DFC_SS_GOTO|GOTO 流程控制陳述式|  
|SQL_DIAG_DFC_SS_INSERT_BULK|INSERT BULK 陳述式|  
|SQL_DIAG_DFC_SS_KILL|KILL 陳述式|  
|SQL_DIAG_DFC_SS_LOAD_DATABASE|LOAD 或 RESTORE DATABASE 陳述式|  
|SQL_DIAG_DFC_SS_LOAD_HEADERONLY|LOAD 或 RESTORE HEADERONLY 陳述式|  
|SQL_DIAG_DFC_SS_LOAD_TABLE|LOAD TABLE 陳述式|  
|SQL_DIAG_DFC_SS_LOAD_TRANSACTION|LOAD 或 RESTORE TRANSACTION 陳述式|  
|SQL_DIAG_DFC_SS_PRINT|PRINT 陳述式|  
|SQL_DIAG_DFC_SS_RAISERROR|RAISERROR 陳述式|  
|SQL_DIAG_DFC_SS_READTEXT|READTEXT 陳述式|  
|SQL_DIAG_DFC_SS_RECONFIGURE|RECONFIGURE 陳述式|  
|SQL_DIAG_DFC_SS_RETURN|RETURN 流程控制陳述式|  
|SQL_DIAG_DFC_SS_SELECT_INTO|SELECT INTO 陳述式|  
|SQL_DIAG_DFC_SS_SET|SET 陳述式 (一般、所有選項)|  
|SQL_DIAG_DFC_SS_SET_IDENTITY_INSERT|SET IDENTITY_INSERT 陳述式|  
|SQL_DIAG_DFC_SS_SET_ROW_COUNT|SET ROWCOUNT 陳述式|  
|SQL_DIAG_DFC_SS_SET_STATISTICS|SET STATISTICS IO 或 SET STATISTICS TIME 陳述式|  
|SQL_DIAG_DFC_SS_SET_TEXTSIZE|SET TEXTSIZE 陳述式|  
|SQL_DIAG_DFC_SS_SETUSER|SETUSER 陳述式|  
|SQL_DIAG_DFC_SS_SET_XCTLVL|SET TRANSACTION ISOLATION LEVEL 陳述式|  
|SQL_DIAG_DFC_SS_SHUTDOWN|SHUTDOWN 陳述式|  
|SQL_DIAG_DFC_SS_TRANS_BEGIN|BEGIN TRAN 陳述式|  
|SQL_DIAG_DFC_SS_TRANS_COMMIT|COMMIT TRAN 陳述式|  
|SQL_DIAG_DFC_SS_TRANS_PREPARE|準備認可分散式交易|  
|SQL_DIAG_DFC_SS_TRANS_ROLLBACK|ROLLBACK TRAN 陳述式|  
|SQL_DIAG_DFC_SS_TRANS_SAVE|SAVE TRAN 陳述式|  
|SQL_DIAG_DFC_SS_TRUNCATE_TABLE|TRUNCATE TABLE 陳述式|  
|SQL_DIAG_DFC_SS_UPDATE_STATISTICS|UPDATE STATISTICS 陳述式|  
|SQL_DIAG_DFC_SS_UPDATETEXT|UPDATETEXT 陳述式|  
|SQL_DIAG_DFC_SS_USE|USE 陳述式|  
|SQL_DIAG_DFC_SS_WAITFOR|WAITFOR 流程控制陳述式|  
|SQL_DIAG_DFC_SS_WRITETEXT|WRITETEXT 陳述式|  
  
## <a name="sqlgetdiagfield-and-table-valued-parameters"></a>SQLGetDiagField 和資料表值參數  
 SQLGetDiagField 可以用來取出兩個診斷欄位： SQL_DIAG_SS_TABLE_COLUMN_NUMBER 和 SQL_DIAG_SS_TABLE_ROW_NUMBER。 這些欄位可協助您判斷哪些值導致與診斷記錄相關聯的錯誤或警告。  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetDiagField 函式](https://go.microsoft.com/fwlink/?LinkId=59352)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
