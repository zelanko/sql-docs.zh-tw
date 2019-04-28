---
title: sp_create_removable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_create_removable
- sp_create_removable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_removable
ms.assetid: 06e36ae5-f70d-4a26-9a7f-ee4b9360b355
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9c2e25b51998d863809a57654b245b1cb63027b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724063"
---
# <a name="spcreateremovable-transact-sql"></a>sp_create_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立抽取式媒體資料庫。 建立三個或更多檔案 (系統目錄資料表和交易記錄各有一個檔案，資料表有一個或多個檔案)，將資料庫放在這些檔案中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 我們建議您改用[CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_create_removable   
   [ @dbname = ] 'dbname',   
   [ @syslogical= ] 'syslogical',   
   [ @sysphysical = ] 'sysphysical',   
   [ @syssize = ] syssize,   
   [ @loglogical = ] 'loglogical',   
   [ @logphysical = ] 'logphysical',   
   [ @logsize = ] logsize,   
   [ @datalogical1 = ] 'datalogical1',   
   [ @dataphysical1 = ] 'dataphysical1',   
   [ @datasize1 = ] datasize1 ,   
   [ @datalogical16 = ] 'datalogical16',   
   [ @dataphysical16 = ] 'dataphysical16',   
   [ @datasize16 = ] datasize16 ]  
```  
  
## <a name="arguments"></a>引數  
`[ @dbname = ] 'dbname'` 是要卸除式媒體上的使用而建立之資料庫的名稱。 *dbname*已**sysname**。  
  
`[ @syslogical = ] 'syslogical'` 是系統目錄資料表所在檔案的邏輯名稱。 *syslogical*已**sysname**。  
  
`[ @sysphysical = ] 'sysphysical'` 這是實體的名稱。 其中包括系統目錄資料表所在檔案的完整路徑。 *sysphysical*已**nvarchar(260)**。  
  
`[ @syssize = ] syssize` 是以 mb 為單位，在系統目錄資料表所在檔案的大小。 *syssize*已**int**。最小*syssize*為 1。  
  
`[ @loglogical = ] 'loglogical'` 這是檔案的包含交易記錄檔邏輯名稱。 *loglogical*已**sysname**。  
  
`[ @logphysical = ] 'logphysical'` 這是實體的名稱。 其中包括交易記錄所在檔案的完整路徑。 *logphysical*已**nvarchar(260)**。  
  
`[ @logsize = ] logsize` 是以 mb 為單位的交易記錄所在檔案的大小。 *logsize*已**int**。最小*logsize*為 1。  
  
`[ @datalogical1 = ] 'datalogical'` 這是檔案的包含資料表邏輯名稱。 *datalogical*已**sysname**。  
  
 必須有 1 至 16 個資料檔。 當預期資料庫較大，必須分散到多個磁碟時，通常會建立一個以上的資料檔。  
  
`[ @dataphysical1 = ] 'dataphysical'` 這是實體的名稱。 其中包括資料表所在檔案的完整路徑。 *dataphysical*已**nvarchar(260)**。  
  
`[ @datasize1 = ] 'datasize'` 是的大小，以 mb 為單位，其中包含資料的資料表。 *datasize*已**int**。最小*datasize*為 1。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 如果您要在抽取式媒體 (如光碟) 上建立資料庫的副本，而且要將資料庫散發給其他使用者，請使用這個預存程序。  
  
## <a name="permissions"></a>Permissions  
 需要 CREATE DATABASE、CREATE ANY DATABASE 或 ALTER ANY DATABASE 權限。  
  
 為了維護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的磁碟控制，通常只有少數登入帳戶有建立資料庫的權限。  
  
### <a name="permissions-on-data-and-log-files"></a>資料和記錄檔的權限  
 每當您在資料庫上執行某些作業時，系統就會針對其資料和記錄檔設定對應的權限。 檔案所在的目錄如有開放權限，上述權限可防止檔案遭到意外竄改。  
  
|資料庫的作業|針對檔案設定的權限|  
|---------------------------|------------------------------|  
|修改以加入新檔案|建立日期|  
|已備份|已附加|  
|已還原|已卸離|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會設定資料和記錄檔的權限。  
  
## <a name="examples"></a>範例  
 下列範例會將 `inventory` 資料庫建立成卸除式資料庫。  
  
```  
EXEC sp_create_removable 'inventory',   
   'invsys',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invsys.mdf'  
, 2,   
   'invlog',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invlog.ldf', 4,  
   'invdata',  
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\invdata.ndf',   
10;  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_certify_removable &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-certify-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
