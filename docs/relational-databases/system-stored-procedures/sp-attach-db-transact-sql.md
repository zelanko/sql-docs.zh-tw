---
title: sp_attach_db （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_db_TSQL
- sp_attach_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_db
ms.assetid: 59bc993e-7913-4091-89cb-d2871cffda95
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 896a4791d1b04de37f57496fd8ff71961a54f7ab
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85874616"
---
# <a name="sp_attach_db-transact-sql"></a>sp_attach_db (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將資料庫附加至伺服器。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]我們建議您改用 CREATE DATABASE *database_name*來進行附加。 如需詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
> [!NOTE]  
>  若要在有一或多個記錄檔有新位置時重建多個記錄檔，請使用 CREATE DATABASE *database_name*進行 ATTACH_REBUILD_LOG。  
  
> [!IMPORTANT]  
>  建議您不要附加或還原來源不明或來源不受信任的資料庫。 這種資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 使用來源不明或來源不受信任的資料庫之前，請先在非實際執行伺服器的資料庫上執行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，同時檢查資料庫中的程式碼，例如預存程序或其他使用者定義程式碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_attach_db [ @dbname= ] 'dbname'  
    , [ @filename1= ] 'filename_n' [ ,...16 ]   
```  
  
## <a name="arguments"></a>引數  
`[ @dbname = ] 'dbnam_ '`這是要附加至伺服器的資料庫名稱。 名稱必須是唯一的。 *dbname*是**sysname**，預設值是 Null。  
  
`[ @filename1 = ] 'filename_n'`這是資料庫檔案的機構名稱，包括路徑。 *filename_n*是**Nvarchar （260）**，預設值是 Null。 您最多可以指定 16 個檔案名稱。 參數名稱會從** \@ filename1**開始，並遞增至** \@ filename16**。 檔案名稱清單至少必須包括主要檔案。 主要檔案包含指向資料庫中其他檔案的系統資料表。 這份清單也必須包括資料庫卸離之後所移動的任何檔案。  
  
> [!NOTE]  
>  這個引數對應到 CREATE DATABASE 陳述式的 FILENAME 參數。 如需詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
>   
>  當您將包含全文檢索目錄檔案的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫附加至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器執行個體時，系統就會從先前的位置附加這些目錄檔案以及其他資料庫檔案，此行為與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的行為相同。 如需詳細資訊，請參閱 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **Sp_attach_db**預存程式只能在先前使用明確**sp_detach_db**作業或複製的資料庫卸離資料庫伺服器的資料庫上執行。 如果您必須指定16個以上的檔案，請針對 [附加] 或 [建立資料庫] *database_name* FOR_ATTACH_REBUILD_LOG 使用 [建立資料庫] *database_name* 。 如需詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
 任何未指定的檔案都假設為在前次的已知位置中。 若要在不同位置使用檔案，您必須指定新位置。  
  
 由較新版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所建立的資料庫無法附加在舊版本中。  
  
> [!NOTE]  
>  無法卸離或附加資料庫快照集。  
  
 當您附加的複寫資料庫是複製而非卸離時，請考慮下列各項：  
  
-   如果您要將資料庫附加至與原始資料庫相同的伺服器執行個體和版本，則不需要其他步驟。  
  
-   如果您將資料庫附加至相同但版本已升級的伺服器執行個體，則必須在附加作業完成後，執行 [sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md) 來升級複寫。  
  
-   如果您將資料庫附加至不同的伺服器執行個體，則不論版本為何，都必須在附加作業完成後，執行 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 來移除複寫。  
  
 當資料庫第一次連接或還原到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體時，資料庫主要金鑰複本 (由服務主要金鑰加密) 尚未儲存在伺服器中。 您必須利用 **OPEN MASTER KEY** 陳述式來解密資料庫主要金鑰 (DMK)。 DMK 解密之後，您便可以選擇利用 **ALTER MASTER KEY REGENERATE** 陳述式來提供服務主要金鑰 (SMK) 所加密的 DMK 複本給伺服器，以在未來啟用自動解密。 當資料庫從舊版升級時，應該會重新產生 DMK 以使用較新的 AES 演算法。 如需重新產生 DMK 的詳細資訊，請參閱 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)。 重新產生 DMK 金鑰以升級至 AES 所需的時間是取決於 DMK 所保護的物件數目而定。 重新產生 DMK 金鑰以升級至 AES 只需執行一次，且不會影響金鑰循環策略中後續的重新產生。  
  
## <a name="permissions"></a>權限  
 如需如何在附加資料庫時處理許可權的詳細資訊，請參閱[CREATE database &#40;SQL Server transact-sql&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會將 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 的檔案附加至目前的伺服器。  
  
```  
EXEC sp_attach_db @dbname = N'AdventureWorks2012',   
    @filename1 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf',   
    @filename2 =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf';  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_removedbreplication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
