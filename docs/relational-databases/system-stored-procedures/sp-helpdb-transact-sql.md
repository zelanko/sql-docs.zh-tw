---
title: sp_helpdb (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7961664bce12a2f1b73e8ca90c6cca11e1075d27
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpdb-transact-sql"></a>sp_helpdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告指定的資料庫或所有資料庫的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@dbname=** ] **'***name***'**  
 這是報告資訊所屬的資料庫名稱。 *名稱*是**sysname**，沒有預設值。 如果*名稱*未指定， **sp_helpdb**報告中的所有資料庫**sys.databases**目錄檢視。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|資料庫名稱。|  
|**db_size**|**nvarchar(13)**|資料庫的總大小。|  
|**擁有者**|**sysname**|資料庫擁有者，例如**sa**。|  
|**dbid**|**smallint**|資料庫識別碼。|  
|**建立**|**nvarchar(11)**|資料庫的建立日期。|  
|**status**|**nvarchar(600)**|資料庫目前所設定的資料庫選項值清單 (以逗號分隔)。<br /><br /> 布林值選項必須已啟用，才會列出。 非布林值選項會列出與對應的值的形式*option_name*=*值*。<br /><br /> 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。|  
|**compatibility_level**|**tinyint**|資料庫相容性層級：60、65、70、80 或 90。|  
  
 如果*名稱*指定，則會顯示指定之資料庫的檔案配置的其他結果集。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nchar(128)**|邏輯檔案名稱。|  
|**fileid**|**smallint**|檔案識別碼。|  
|**filename**|**nchar(260)**|作業系統檔案名稱 (實體檔案名稱)。|  
|**filegroup**|**nvarchar(128)**|檔案所屬的檔案群組。<br /><br /> NULL = 檔案是記錄檔。 它永遠不在檔案群組中。|  
|**size**|**nvarchar(18)**|檔案大小 (以 MB 為單位)。|  
|**maxsize**|**nvarchar(18)**|檔案所能成長的大小上限。 這個欄位中的 UNLIMITED 值指出，檔案將成長到磁碟已滿。|  
|**成長**|**nvarchar(18)**|檔案的成長遞增。 這表示每次需要新空間時，檔案所增加的空間量。|  
|**使用方式**|**varchar(9)**|檔案的使用方式。 對於資料檔中，這個值是 **'僅限資料'** 和記錄檔的值是**僅限記錄'**。|  
  
## <a name="remarks"></a>備註  
 **狀態**結果中的資料行集的選項已設定為 ON 的資料庫中的報表。 所有資料庫選項不會都報告**狀態**資料行。 若要查看目前的資料庫選項設定的完整清單，請使用**sys.databases**目錄檢視。  
  
## <a name="permissions"></a>Permissions  
 指定單一資料庫時，成員資格**公用**所需的資料庫中的 role。 當未不指定任何資料庫時中的成員資格**公用**中的角色**主要**資料庫是必要元件。  
  
 如果無法存取資料庫， **sp_helpdb**可能會顯示錯誤訊息 15622 和許多資料庫的資訊。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-information-about-a-single-database"></a>A. 傳回單一資料庫的相關資訊  
 下列範例會顯示 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的相關資訊。  
  
```sql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>B. 傳回所有資料庫的相關資訊  
 下列範例會顯示執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的伺服器之所有資料庫的相關資訊。  
  
```sql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
