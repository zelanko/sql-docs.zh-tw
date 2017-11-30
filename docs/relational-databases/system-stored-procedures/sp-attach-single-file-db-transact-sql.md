---
title: "sp_attach_single_file_db (TRANSACT-SQL) |Microsoft 文件"
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
- sp_attach_single_file_db
- sp_attach_single_file_db_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_attach_single_file_db
ms.assetid: 13bd1044-9497-4293-8390-1f12e6b8e952
caps.latest.revision: "68"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: de907b1bd4a60c4b3419635c22e204af8f581d0c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spattachsinglefiledb-transact-sql"></a>sp_attach_single_file_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將只有一個資料檔的資料庫附加至目前的伺服器。 **sp_attach_single_file_db**不能與多個資料檔案。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]我們建議您改用 CREATE DATABASE *database_name* FOR ATTACH 改為。 如需詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。 請勿在複寫資料庫上使用此程序。  
  
> [!IMPORTANT]  
>  建議您不要附加或還原來源不明或來源不受信任的資料庫。 這種資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 使用來源不明或來源不受信任的資料庫之前，請先在非實際執行伺服器的資料庫上執行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，同時檢查資料庫中的程式碼，例如預存程序或其他使用者定義程式碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_attach_single_file_db [ @dbname= ] 'dbname'  
    , [ @physname= ] 'physical_name'  
```  
  
## <a name="arguments"></a>引數  
 [  **@dbname=** ] **'***dbname***'**  
 這是要附加至伺服器的資料庫名稱。 名稱必須是唯一的。 *dbname*是**sysname**，預設值是 NULL。  
  
 [  **@physname=** ] **'***physical_name***'**  
 這是資料庫檔案的實體名稱，其中包括路徑。 *physical_name*是**nvarchar （260)**，預設值是 NULL。  
  
> [!NOTE]  
>  這個引數對應到 CREATE DATABASE 陳述式的 FILENAME 參數。 如需詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
 當您將包含全文檢索目錄檔案的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫附加至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器執行個體時，系統就會從先前的位置附加這些目錄檔案以及其他資料庫檔案，此行為與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的行為相同。 如需詳細資訊，請參閱 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 使用**sp_attach_single_file_db**只在先前卸離從伺服器使用明確的資料庫上**sp_detach_db**作業或對已複製的資料庫。  
  
 **sp_attach_single_file_db**只適用於具有單一記錄檔的資料庫。 當**sp_attach_single_file_db**將資料庫附加至伺服器，它會建立新的記錄檔。 如果資料庫是唯讀的，就會在先前的位置建立記錄檔。  
  
> [!NOTE]  
>  無法卸離或附加資料庫快照集。  
  
 請勿在複寫資料庫上使用此程序。  
  
## <a name="permissions"></a>Permissions  
 如需附加資料庫時，如何處理權限資訊，請參閱[CREATE DATABASE &#40;SQL Server TRANSACT-SQL &#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
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
  
## <a name="see-also"></a>請參閱  
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
