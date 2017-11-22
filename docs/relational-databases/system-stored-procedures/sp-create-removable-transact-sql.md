---
title: "sp_create_removable (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_create_removable
- sp_create_removable_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_create_removable
ms.assetid: 06e36ae5-f70d-4a26-9a7f-ee4b9360b355
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d16ba597797bb5a89265856e9ced307e9801ce46
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="spcreateremovable-transact-sql"></a>sp_create_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立抽取式媒體資料庫。 建立三個或更多檔案 (系統目錄資料表和交易記錄各有一個檔案，資料表有一個或多個檔案)，將資料庫放在這些檔案中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]我們建議您改用[CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md)改為。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
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
 [  **@dbname=** ] **'***dbname***'**  
 這是您要建立以便在抽取式媒體上使用的資料庫名稱。 *dbname*是**sysname**。  
  
 [  **@syslogical=** ] **'***syslogical***'**  
 這是系統目錄資料表所在檔案的邏輯名稱。 *syslogical*是**sysname**。  
  
 [  **@sysphysical=** ] **'***sysphysical***'**  
 這是實體名稱。 其中包括系統目錄資料表所在檔案的完整路徑。 *sysphysical*是**nvarchar （260)**。  
  
 [  **@syssize=** ] *syssize*  
 這是系統目錄資料表所在檔案的大小 (以 MB 為單位)。 *syssize*是**int**。最小值*syssize*為 1。  
  
 [  **@loglogical=** ] **'***loglogical***'**  
 這是交易記錄所在檔案的邏輯名稱。 *loglogical*是**sysname**。  
  
 [  **@logphysical=** ] **'***logphysical***'**  
 這是實體名稱。 其中包括交易記錄所在檔案的完整路徑。 *logphysical*是**nvarchar （260)**。  
  
 [  **@logsize=** ] *logsize*  
 這是交易記錄所在檔案的大小 (以 MB 為單位)。 *logsize*是**int**。最小值*logsize*為 1。  
  
 [  **@datalogical1=** ] **'***datalogical***'**  
 這是資料表所在檔案的邏輯名稱。 *datalogical*是**sysname**。  
  
 必須有 1 至 16 個資料檔。 當預期資料庫較大，必須分散到多個磁碟時，通常會建立一個以上的資料檔。  
  
 [  **@dataphysical1=** ] **'***dataphysical***'**  
 這是實體名稱。 其中包括資料表所在檔案的完整路徑。 *dataphysical*是**nvarchar （260)**。  
  
 [  **@datasize1=** ] **'***datasize***'**  
 這是資料表所在檔案的大小 (以 MB 為單位)。 *datasize*是**int**。最小值*datasize*為 1。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_certify_removable &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-certify-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_dbremove &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [sp_detach_db &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
