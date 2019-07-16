---
title: sp_add_log_file_recover_suspect_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_file_recover_suspect_db_TSQL
- sp_add_log_file_recover_suspect_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_file_recover_suspect_db
ms.assetid: b41ca3a5-7222-4c22-a012-e66a577a82f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9f951aaee96bccf0c2876c781aaebdd2a009b51d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140482"
---
# <a name="spaddlogfilerecoversuspectdb-transact-sql"></a>sp_add_log_file_recover_suspect_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  當因為記錄空間不足 (9002 錯誤) 而無法完成資料庫的復原作業時，將記錄檔加入檔案群組中。 加入檔案之後， **sp_add_log_file_recover_suspect_db**會關閉受到質疑的設定，並完成復原的資料庫。 參數是一樣的 ALTER DATABASE *database_name* ADD LOG FILE。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_log_file_recover_suspect_db [ @dbName= ] 'database' ,   
    [ @name = ] 'logical_file_name' ,   
    [ @filename= ] 'os_file_name' ,   
    [ @size = ] 'size' ,   
    [ @maxsize = ] 'max_size' ,   
    [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>引數  
`[ @dbName = ] 'database'` 是資料庫的名稱。 *資料庫*已**sysname**，沒有預設值。  
  
`[ @name = ] 'logical_file_name'` 是中使用的名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]參考檔案時。 在伺服器中，這個名稱必須是唯一的。 *logical_file_name*已**nvarchar(260)** ，沒有預設值。  
  
`[ @filename = ] 'os_file_name'` 路徑和檔案名稱用於作業系統檔案。 這個檔案必須在安裝了 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的伺服器中。 *os_file_name*已**nvarchar(260)** ，沒有預設值。  
  
`[ @size = ] 'size_ '` 是檔案初始大小。 *大小*已**nvarchar(20)** ，預設值是 NULL。 請指定一個整數，不包括小數點。 您可以利用 MB 和 KB 後置詞來指定百萬位元組或千位元組。 預設值是 MB。 最小值是 512 KB。 如果*大小*未指定，預設值為 1 MB。  
  
`[ @maxsize = ] 'max_size_ '` 是檔案所能成長的大小上限。 *max_size*已**nvarchar(20)** ，預設值是 NULL。 請指定一個整數，不包括小數點。 您可以利用 MB 和 KB 後置詞來指定百萬位元組或千位元組。 預設值是 MB。  
  
 如果*max_size*未指定，檔案會成長到磁碟已滿。 當磁碟將滿時，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔會警告管理員。  
  
`[ @filegrowth = ] 'growth_increment_ '` 是每次需要新空間時新增至檔案數量。 *growth_increment*已**nvarchar(20)** ，預設值是 NULL。 0 值表示不成長。 請指定一個整數，不包括小數點。 您可以用 MB、KB 或百分比 (%) 來指定這個值。 當指定 % 時，成長的遞增是增量發生時之指定的檔案大小百分比。 如果指定的數字不含 MB、KB 或 % 後置詞，預設值是 MB。  
  
 如果*growth_increment*是 NULL，預設值是 10%，而且最小值為 64 KB。 指定的大小會捨入到最接近 64 KB。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>Permissions  
 執行權限預設為隸屬**sysadmin**固定的伺服器角色。 這些權限無法轉讓。  
  
## <a name="examples"></a>範例  
 在下列範例中，`db1` 資料庫在復原期間，因記錄空間不足 (9002 錯誤) 而標示為受到質疑。  
  
```  
USE master;  
GO  
EXEC sp_add_log_file_recover_suspect_db db1, logfile2,  
'C:\Program Files\Microsoft SQL  
    Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_logfile2.ldf',   
    '1MB';  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_add_data_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-data-file-recover-suspect-db-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
