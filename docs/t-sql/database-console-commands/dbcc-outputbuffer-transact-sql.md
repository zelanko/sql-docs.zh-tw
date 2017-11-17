---
title: "DBCC OUTPUTBUFFER (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC OUTPUTBUFFER
- OUTPUTBUFFER_TSQL
- OUTPUTBUFFER
- DBCC_OUTPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC OUTPUTBUFFER statement
- output buffers
- current output buffer
ms.assetid: e912a06d-9fde-4e26-b057-801255d79504
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: de51ee1a87f37e8fcdf97e23be0d2fb9701e9433
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-outputbuffer-transact-sql"></a>DBCC OUTPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

傳回目前的輸出緩衝區，以十六進位和 ASCII 格式指定*session_id*。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
```sql
DBCC OUTPUTBUFFER ( session_id [ , request_id ])  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
 *session_id*  
 這是每個使用中的主要連接所關聯的工作階段識別碼。  
  
 *request_id*  
 這是要在目前工作階段內搜尋的確實要求 (批次)。  
 下列查詢會傳回*request_id*:  
  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
  
 取代所有提及的  
 接受即將指定的選項。  
  
 NO_INFOMSGS  
 抑制所有嚴重性層級在 0 到 10 的參考用訊息。  
  
## <a name="remarks"></a>備註  
DBCC OUTPUTBUFFER 會顯示傳送至指定的用戶端的結果 (*session_id*)。 如果是不包含輸出資料流的處理序，便會傳回錯誤訊息。
  
若要顯示執行之後傳回 DBCC OUTPUTBUFFER 所顯示之結果的陳述式，請執行 DBCC INPUTBUFFER。
  
## <a name="result-sets"></a>結果集  
DBCC OUTPUTBUFFER 會傳回下列值 (值可能不同)：
  
```sql
Output Buffer                                                              
------------------------------------------------------------------------   
01fb8028:  04 00 01 5f 00 00 00 00 e3 1b 00 01 06 6d 00 61  ..._.........m.a  
01fb8038:  00 73 00 74 00 65 00 72 00 06 6d 00 61 00 73 00  .s.t.e.r..m.a.s.  
'...'  
01fb8218:  04 17 00 00 00 00 00 d1 04 18 00 00 00 00 00 d1  ................  
01fb8228:   .  
  
(33 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。
  
## <a name="examples"></a>範例  
下列範例會傳回假設的工作階段識別碼 `52` 之目前輸出緩衝區資訊。
  
```sql
DBCC OUTPUTBUFFER (52);  
```  
  
## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  

