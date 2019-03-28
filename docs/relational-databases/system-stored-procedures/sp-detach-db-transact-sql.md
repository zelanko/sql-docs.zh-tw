---
title: sp_detach_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_detach_db
- sp_detach_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_detach_db
- detaching databases [SQL Server]
ms.assetid: abcb1407-ff78-4c76-b02e-509c86574462
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b5dfd9cf062e5767606d83c3beb8a25b36387f1
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538220"
---
# <a name="spdetachdb-transact-sql"></a>sp_detach_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從伺服器執行個體中卸離目前未使用的資料庫，並於卸離之前在所有資料表上選擇性地執行 UPDATE STATISTICS。  
  
> [!IMPORTANT]  
>  必須是未發行的複寫資料庫，才能予以卸離。 如需詳細資訊，請參閱本主題後面的＜備註＞一節。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_detach_db [ @dbname= ] 'database_name'   
    [ , [ @skipchecks= ] 'skipchecks' ]   
    [ , [ @keepfulltextindexfile = ] 'KeepFulltextIndexFile' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @dbname = ] 'database_name'` 是要卸離資料庫的名稱。 *database_name*已**sysname**值，預設值是 NULL。  
  
`[ @skipchecks = ] 'skipchecks'` 指定是否要跳過或執行 UPDATE STATISTIC。 *skipchecks*已**nvarchar(10**值，預設值是 NULL。 若要跳過更新統計資料，請指定 **，則為 true**。 若要明確地執行 UPDATE STATISTICS，指定**false**。  
  
 根據預設，系統會執行 UPDATE STATISTICS 來更新資料表和索引之資料的相關資訊。 對於要移至唯讀媒體的資料庫而言，執行 UPDATE STATISTICS 很有用。  
  
`[ @keepfulltextindexfile = ] 'KeepFulltextIndexFile'` 指定全文檢索索引相關聯的檔案與要卸離的資料庫不會捨棄在資料庫卸離作業。 *KeepFulltextIndexFile*已**nvarchar(10**值，預設值是**true**。 如果*KeepFulltextIndexFile*是**false**、 與資料庫相關聯的所有全文檢索索引檔案和全文檢索索引的中繼資料已卸除，除非資料庫為唯讀。 如果是 NULL 或 **，則為 true**，全文檢索相關中繼資料會保留。  
  
> [!IMPORTANT]
>  **@keepfulltextindexfile**的未來版本將移除參數[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請勿在新的開發工作中使用此參數，並且盡快修改使用此參數的應用程式。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 卸離資料庫時，就會卸除其所有中繼資料。 如果資料庫是任何登入帳戶的預設資料庫**主要**即成為其預設資料庫。  
  
> [!NOTE]  
>  如需有關如何檢視所有登入帳戶的預設資料庫的資訊，請參閱 < [sp_helplogins &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)。 如果您有必要的權限，您可以使用[ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)指派新的預設資料庫的登入。  
  
## <a name="restrictions"></a>限制  
 如果出現下列的任何狀況，您便無法卸離資料庫：  
  
-   資料庫目前正在使用中。 如需詳細資訊，請參閱本主題後面的＜取得獨佔存取權＞一節。  
  
-   如果已複寫，就表示已發行資料庫。  
  
     您可以卸離資料庫之前，您必須執行停用發行[sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)。  
  
    > [!NOTE]  
    >  如果您無法使用 **sp_replicationdboption**，可執行 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)來移除複寫。  
  
-   資料庫有資料庫快照集存在。  
  
     在卸離資料庫之前，您必須先卸除它的所有快照集。 如需詳細資訊，請參閱 [卸除資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)執行個體。  
  
    > [!NOTE]  
    >  無法卸離或附加資料庫快照集。  
  
-   資料庫正在進行鏡像。  
  
     在資料庫鏡像工作階段結束之前，您無法卸離資料庫。 如需詳細資訊，請參閱 [移除資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)＞。  
  
-   資料庫受質疑。  
  
     您必須讓受質疑的資料庫進入緊急模式，然後才能卸離資料庫。 如需有關如何使資料庫進入緊急模式的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  
  
-   此資料庫是系統資料庫。  
  
## <a name="obtaining-exclusive-access"></a>取得獨佔存取權  
 您需要有資料庫的獨佔存取權才能卸離資料庫。 如果您要卸離的資料庫正在使用中，請先將資料庫設為 SINGLE_USER 模式以取得獨佔存取權，才能進行卸離。  
  
 例如，下列`ALTER DATABASE`陳述式會取得獨佔存取權[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫之後中斷資料庫的所有目前的使用者。  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  若要強制現行使用者移出資料庫立即或在指定的秒數內同時使用 ROLLBACK 選項：ALTER DATABASE *database_name* SET SINGLE_USER WITH ROLLBACK *rollback_option*。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  
  
## <a name="reattaching-a-database"></a>重新附加資料庫  
 卸離的檔案會保留下來，您可以利用 CREATE DATABASE 來重新附加它 (使用 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 選項)。 您可以將這些檔案移到另一部伺服器，將它附加在那裡。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定伺服器角色或成員資格**db_owner**資料庫的角色。  
  
## <a name="examples"></a>範例  
 下列範例會卸離[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]與資料庫*skipchecks*設為 true。  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
 下列範例會卸離 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫並保留全文檢索索引檔和全文檢索索引的中繼資料。 這個命令會執行 UPDATE STATISTICS，這是預設行為。  
  
```  
exec sp_detach_db @dbname='AdventureWorks2012'  
    , @keepfulltextindexfile='true';  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [卸離資料庫](../../relational-databases/databases/detach-a-database.md)  
  
  
