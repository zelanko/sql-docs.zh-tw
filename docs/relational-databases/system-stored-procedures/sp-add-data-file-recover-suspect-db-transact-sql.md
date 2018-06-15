---
title: sp_add_data_file_recover_suspect_db (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_data_file_recover_suspect_db
- sp_add_data_file_recover_suspect_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_data_file_recover_suspect_db
ms.assetid: b25262aa-a228-48b7-8739-6581c760b171
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 13c08441680744d38f870fc5b6ebd5d7a1e20c91
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239158"
---
# <a name="spadddatafilerecoversuspectdb-transact-sql"></a>sp_add_data_file_recover_suspect_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  當因為檔案群組空間不足 (1105 錯誤) 而無法完成資料庫的復原作業時，將資料檔加入檔案群組中。 加入檔案之後，這個預存程序會關閉受到質疑的設定，再完成資料庫的復原。 參數會與 ALTER DATABASE 相同*database_name*加入檔案。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_data_file_recover_suspect_db [ @dbName= ] 'database'   
    , [ @filegroup = ] 'filegroup_name'   
    , [ @name = ] 'logical_file_name'   
    , [ @filename= ] 'os_file_name'   
    , [ @size = ] 'size'   
    , [ @maxsize = ] 'max_size'   
    , [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>引數  
 [ **@dbName=** ] **'***database* **'**  
 這是資料庫的名稱。 *資料庫*是**sysname**，沒有預設值。  
  
 [ **@filegroup=** ] **'***filegroup_name* **'**  
 這是檔案要加入其中的檔案群組。 *filegroup_name*是**nvarchar （260)**，預設值是 NULL，表示主要檔案。  
  
 [ **@name=** ] **'***logical_file_name* **'**  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中用來參考檔案的名稱。 在伺服器中，這個名稱必須是唯一的。 *邏輯檔案名稱*是**nvarchar （260)**，沒有預設值。  
  
 [ **@filename=** ] **'***os_file_name* **'**  
 這是作業系統針對檔案所用的路徑和檔案名稱。 這個檔案必須在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體中。 *os_file_name*是**nvarchar （260)**，沒有預設值。  
  
 [ **@size=** ] **'***size* **'**  
 這是檔案的初始大小。 *大小*是**nvarchar （20)**，預設值是 NULL。 請指定一個整數，不包括小數點。 您可以利用 MB 和 KB 後置詞來指定百萬位元組或千位元組。 預設值是 MB。 最小值是 512 KB。 如果*大小*未指定，預設值為 1 MB。  
  
 [ **@maxsize=** ] **'***max_size* **'**  
 這是檔案所能成長的大小上限。 *max_size*是**nvarchar （20)**，預設值是 NULL。 請指定一個整數，不包括小數點。 您可以利用 MB 和 KB 後置詞來指定百萬位元組或千位元組。 預設值是 MB。  
  
 如果*max_size*未指定，檔案可以成長到磁碟已滿。 當磁碟將滿時，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔會警告管理員。  
  
 [ **@filegrowth=** ] **'***growth_increment* **'**  
 這是每次需要新空間時，檔案所增加的空間量。 *growth_increment*是**nvarchar （20)**，預設值是 NULL。 0 值表示不成長。 請指定一個整數，不包括小數點。 您可以用 MB、KB 或百分比 (%) 來指定這個值。 當指定 % 時，成長的遞增是增量發生時之指定的檔案大小百分比。 如果指定的數字不含 MB、KB 或 % 後置詞，預設值是 MB。  
  
 如果*growth_increment*是 NULL，則預設值是 10%，而且最小值是 64 KB。 指定的大小會捨入到最接近 64 KB。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="permissions"></a>Permissions  
 預設執行權限的成員**sysadmin**固定的伺服器角色。 這些權限無法轉讓。  
  
## <a name="examples"></a>範例  
 在下列範例中，`db1` 資料庫在復原期間，因 `fg1` 檔案群組空間不足 (1105 錯誤) 而標示為受到質疑。  
  
```  
USE master;  
GO  
EXEC sp_add_data_file_recover_suspect_db db1, fg1, file2,  
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_file2.mdf', '1MB';  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
