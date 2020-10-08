---
description: sp_detach_db (Transact-SQL)
title: sp_detach_db (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6829fff1f535a0e0d55b8dd849c67b0b197c4e48
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810835"
---
# <a name="sp_detach_db-transact-sql"></a>sp_detach_db (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @dbname = ] 'database_name'` 這是要卸離的資料庫名稱。 *database_name* 是 **sysname** 值，預設值是 Null。  
  
`[ @skipchecks = ] 'skipchecks'` 指定是否略過或執行更新統計資料。 *skipchecks* 是 **Nvarchar (10) ** 值，預設值是 Null。 若要略過 UPDATE STATISTICS，請指定 **true**。 若要明確地執行更新統計資料，請指定 **false**。  
  
 根據預設，系統會執行 UPDATE STATISTICS 來更新資料表和索引之資料的相關資訊。 對於要移至唯讀媒體的資料庫而言，執行 UPDATE STATISTICS 很有用。  
  
`[ @keepfulltextindexfile = ] 'KeepFulltextIndexFile'` 指定與要卸離之資料庫相關聯的全文檢索索引檔案，將不會在資料庫卸離作業期間卸載。 *>keepfulltextindexfile* 是 **Nvarchar (10) ** 值，預設值為 **true**。 如果 *>keepfulltextindexfile* 為 **false**，則會卸載與資料庫相關聯的所有全文檢索索引檔案和全文檢索索引的中繼資料，除非資料庫是唯讀的。 如果為 Null 或 **true**，則會保留全文檢索相關的中繼資料。  
  
> [!IMPORTANT]
>  未來的版本將移除** \@ >keepfulltextindexfile**參數 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 請勿在新的開發工作中使用此參數，並且盡快修改使用此參數的應用程式。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 卸離資料庫時，就會卸除其所有中繼資料。 如果資料庫是任何登入帳戶的預設資料庫， **master** 會成為其預設資料庫。  
  
> [!NOTE]  
>  如需如何查看所有登入帳戶之預設資料庫的詳細資訊，請參閱 [sp_helplogins &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)。 如果您有必要的許可權，您可以使用 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 將新的預設資料庫指派給登入。  
  
## <a name="restrictions"></a>限制  
 如果出現下列的任何狀況，您便無法卸離資料庫：  
  
-   資料庫目前正在使用中。 如需詳細資訊，請參閱本主題後面的＜取得獨佔存取權＞一節。  
  
-   如果已複寫，就表示已發行資料庫。  
  
     在卸離資料庫之前，您必須執行 [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)來停用發行。  
  
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

 將資料庫設為 SINGLE_USER 之前，請先確定 AUTO_UPDATE_STATISTICS_ASYNC 選項是否設為 OFF。 此選項設為 ON 時，更新統計資料的背景執行緒會取得資料庫連接，而您就無法以單一使用者模式存取資料庫。 如需詳細資訊，請參閱 [將資料庫設定為單一使用者模式](../databases/set-a-database-to-single-user-mode.md)。

 例如，下列語句會 `ALTER DATABASE` [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 在所有目前使用者與資料庫中斷連線之後，取得資料庫的獨佔存取權。  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012  
SET SINGLE_USER;  
GO  
```  
  
> [!NOTE]  
>  若要立即或在指定的秒數內強制讓目前的使用者離開資料庫，請同時使用 ROLLBACK 選項： ALTER DATABASE *database_name* SET SINGLE_USER WITH rollback *rollback_option*。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  
  
## <a name="reattaching-a-database"></a>重新附加資料庫  
 卸離的檔案會保留下來，您可以利用 CREATE DATABASE 來重新附加它 (使用 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 選項)。 您可以將這些檔案移到另一部伺服器，將它附加在那裡。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員（sysadmin** ）固定伺服器角色中的成員資格，或是資料庫之 **db_owner** 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 將 *skipchecks* 設為 true 的資料庫卸離。  
  
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
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [卸離資料庫](../../relational-databases/databases/detach-a-database.md)  
  
