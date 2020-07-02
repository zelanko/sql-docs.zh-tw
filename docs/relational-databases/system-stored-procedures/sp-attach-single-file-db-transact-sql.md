---
title: sp_attach_single_file_db （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_single_file_db
- sp_attach_single_file_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_single_file_db
ms.assetid: 13bd1044-9497-4293-8390-1f12e6b8e952
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3d3a7a396c381facb76eb3abcc0d7fe67e5991ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716188"
---
# <a name="sp_attach_single_file_db-transact-sql"></a>sp_attach_single_file_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  將只有一個資料檔的資料庫附加至目前的伺服器。 **sp_attach_single_file_db**不能與多個資料檔案搭配使用。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]我們建議您改用 CREATE DATABASE *database_name*來進行附加。 如需詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。 請勿在複寫資料庫上使用此程序。  
  
> [!IMPORTANT]  
>  建議您不要附加或還原來源不明或來源不受信任的資料庫。 這種資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 使用來源不明或來源不受信任的資料庫之前，請先在非實際執行伺服器的資料庫上執行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，同時檢查資料庫中的程式碼，例如預存程序或其他使用者定義程式碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_attach_single_file_db [ @dbname= ] 'dbname'  
    , [ @physname= ] 'physical_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @dbname = ] 'dbname'`這是要附加至伺服器的資料庫名稱。 名稱必須是唯一的。 *dbname*是**sysname**，預設值是 Null。  
  
`[ @physname = ] 'physical_name'`這是資料庫檔案的機構名稱，包括路徑。 *physical_name*是**Nvarchar （260）**，預設值是 Null。  
  
> [!NOTE]  
>  這個引數對應到 CREATE DATABASE 陳述式的 FILENAME 參數。 如需詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
 當您將包含全文檢索目錄檔案的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫附加至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器執行個體時，系統就會從先前的位置附加這些目錄檔案以及其他資料庫檔案，此行為與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的行為相同。 如需詳細資訊，請參閱 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 只有在先前使用明確**sp_detach_db**作業或複製的資料庫卸離伺服器的資料庫上，才使用**sp_attach_single_file_db** 。  
  
 **sp_attach_single_file_db**只適用于具有單一記錄檔的資料庫。 當**sp_attach_single_file_db**將資料庫附加到伺服器時，它會建立新的記錄檔。 如果資料庫是唯讀的，就會在先前的位置建立記錄檔。  
  
> [!NOTE]  
>  無法卸離或附加資料庫快照集。  
  
 請勿在複寫資料庫上使用此程序。  
  
## <a name="permissions"></a>權限  
 如需如何在附加資料庫時處理許可權的詳細資訊，請參閱[CREATE database &#40;SQL Server transact-sql&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會卸離 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，再從 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中，將一個檔案附加至目前的伺服器。  
  
```  
USE master;  
GO  
EXEC sp_detach_db @dbname = 'AdventureWorks2012';  
EXEC sp_attach_single_file_db @dbname = 'AdventureWorks2012',   
    @physname =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf';  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
