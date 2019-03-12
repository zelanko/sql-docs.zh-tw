---
title: DBCC INPUTBUFFER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
author: pmasl
ms.author: umajay
manager: craigg
ms.openlocfilehash: 22891968234e0ad81e95e6aa78c76a2f8e5d4910
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685375"
---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

顯示從用戶端傳送至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體的上一個陳述式。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引數  
*session_id*  
這是每個使用中的主要連接所關聯的工作階段識別碼。  
  
*request_id*  
這是要在目前工作階段內搜尋的確實要求 (批次)。  

下列查詢會傳回 *request_id*：  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
取代所有提及的  
啟用要指定的選項。  
  
NO_INFOMSGS  
抑制所有嚴重性層級在 0 到 10 的參考用訊息。  
  
## <a name="result-sets"></a>結果集  
DBCC INPUTBUFFER 會傳回含有下列資料行的資料列集。
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**EventType**|**nvarchar(30)**|事件類型。 這可能會是「RPC 事件」或「語言事件」。 如果未偵測到上一個事件，輸出將為「無事件」。|  
|**參數**|**smallint**|0 = 文字<br /><br /> 1- *n* = 參數|  
|**EventInfo**|**nvarchar(4000)**|如果 **EventType** 是 RPC，**EventInfo**只會包含程序名稱。 如果 **EventType** 是「語言」，便只會顯示事件的前 4000 個字元。|  
  
例如，當緩衝區內的最後一個事件是 DBCC INPUTBUFFER(11)，DBCC INPUTBUFFER 會傳回下列結果集。
  
```
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  

> [!NOTE]
> 從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 開始，請使用 [sys.dm_exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) 來傳回提交至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之執行個體的相關陳述式資訊。

## <a name="permissions"></a>[權限]  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，需要下列其中之一：
-   使用者必須是系統管理員 **sysadmin** 固定伺服器角色的成員。  
-   使用者必須擁有 VIEW SERVER STATE 權限。  
-   *session_id* 必須與執行命令的工作階段識別碼相同。 若要判斷工作階段識別碼，請執行下列查詢：  
  
```sql
SELECT @@spid;  
```
  
在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 進階和業務關鍵層上需要資料庫中的 VIEW DATABASE STATE 權限。 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 標準、基本，和一般用途層上需要 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 系統管理員帳戶。
  
## <a name="examples"></a>範例  
下列範例會在先前的連接執行長交易時，在第二個連接上執行 `DBCC INPUTBUFFER`。
  
```sql
CREATE TABLE dbo.T1 (Col1 int, Col2 char(3));  
GO  
DECLARE @i int = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS char(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>另請參閱  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  
