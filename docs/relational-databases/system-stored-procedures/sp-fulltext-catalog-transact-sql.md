---
title: sp_fulltext_catalog (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_catalog_TSQL
- sp_fulltext_catalog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_catalog
ms.assetid: e49b98e4-d1f1-42b2-b16f-eb2fc7aa1cf5
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fccb384317102ef2818a49ef09c5faeb0fc42eb1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spfulltextcatalog-transact-sql"></a>sp_fulltext_catalog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  建立和卸除全文檢索目錄，以及啟動和停止目錄的索引動作。 每個資料庫都可以建立多個全文檢索目錄。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)， [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)，和[DROP FULLTEXT CATALOG](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_fulltext_catalog [ @ftcat= ] 'fulltext_catalog_name' ,   
     [ @action= ] 'action'   
     [ , [ @path= ] 'root_directory' ]   
```  
  
## <a name="arguments"></a>引數  
 [ **@ftcat=**] **'***fulltext_catalog_name***'**  
 這是全文檢索目錄的名稱。 每個資料庫的目錄名稱都必須是唯一的。 *fulltext_catalog_name*是**sysname**。  
  
 [  **@action=**] **'***動作***'**  
 這是要執行的動作。 *動作*是**varchar （20)**，而且可以是下列值之一。  
  
> [!NOTE]  
>  您可以依照需要來建立、卸除和修改全文檢索目錄。 不過，請避免同時變更多個目錄的結構描述。 可以使用執行這些動作**sp_fulltext_table**預存程序，是建議的方式。  
  
|Value|Description|  
|-----------|-----------------|  
|**建立**|檔案系統中建立空白的新全文檢索目錄，並將相關聯的資料列中**sysfulltextcatalogs**與*fulltext_catalog_name*和*root_directory*，如果有的話，則值。 *fulltext_catalog_name*資料庫內必須是唯一。|  
|**Drop**|卸除*fulltext_catalog_name*從檔案系統中移除，並刪除相關聯的資料列中**sysfulltextcatalogs**。 如果這個目錄包含一個或多個資料表的索引，這個動作便會失敗。 **sp_fulltext_table** '*table_name*'，'drop' 應該執行以卸除目錄的資料表。<br /><br /> 如果目錄不存在，就會出現錯誤。|  
|**start_incremental**|啟動的累加母體擴展*fulltext_catalog_name*。 如果目錄不存在，就會出現錯誤。 如果全文檢索索引擴展已在使用中，便會顯示一則警告，但不會進行任何擴展動作。 累加母體擴展變更的資料列擷取全文檢索索引，前提是有**時間戳記**表格中的資料行進行全文檢索索引。|  
|**start_full**|啟動完整母體擴展*fulltext_catalog_name*。 此時會針對全文檢索索引擷取與這份全文檢索目錄相關聯之每份資料表的每個資料列，即使它們已建立索引也一樣。|  
|**停止**|停止的索引母體擴展*fulltext_catalog_name*。 如果目錄不存在，就會出現錯誤。 如果母體擴展已停止，便不會顯示任何警告。|  
|**Rebuild**|重建*fulltext_catalog_name*。 重建目錄時，會刪除現有的目錄，並就地建立新的目錄。 具有全文檢索索引參考的所有資料表都會與新目錄產生關聯。 重建會重設資料庫系統資料表中的全文檢索中繼資料。<br /><br /> 如果變更追蹤為 OFF，重建並不會重新擴展新建的全文檢索目錄。 在此情況下，若要重新擴展，請執行**sp_fulltext_catalog**與**start_incremental**或**start_incremental**動作。|  
  
 [ **@path=**] **'***root_directory***'**  
 為根目錄 （不是完整實體路徑）**建立**動作。 *root_directory*是**nvarchar （100)** 且具有預設值是 NULL，表示使用安裝程式所指定的預設位置。 這是在 Mssql 目錄; 中的 Ftdata 子目錄例如，C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\MSSQL\FTData。 指定的根目錄必須在相同電腦的磁碟機中，它不只是磁碟機代號，也不能是相對路徑。 網路磁碟機、卸除式磁碟機、磁碟片及 UNC 路徑都不在支援範圍內。 全文檢索目錄必須建立在與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體相關聯的本機硬碟中。  
  
 **@path** 有效時，才*動作*是**建立**。 針對動作以外**建立**(**停止**，**重建**等等)， **@path**必須是 NULL 或省略。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體是叢集中的虛擬伺服器，指定的全文檢索目錄之目錄就必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源所依賴的共用硬碟中。 如果@path未指定，預設目錄之目錄的位置是共用的磁碟機中安裝虛擬伺服器時所指定的目錄中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 **Start_incremental**動作可用來建立完成中的全文檢索資料快照集*fulltext_catalog_name*。 **Start_incremental**動作可用來重新建立索引只變更的資料庫的資料列。 只有當資料表具有類型的資料行，就可以套用的累加母體擴展**時間戳記**。 如果全文檢索目錄中的資料表不包含類型的資料行**時間戳記**，資料表就會進行完整母體擴展。  
  
 全文檢索目錄和索引資料會儲存在全文檢索目錄之目錄下所建立的檔案中。 全文檢索類別目錄會建立為目錄中指定的目錄的子目錄**@path**或伺服器預設全文檢索目錄的目錄中如果**@path**不是指定。 全文檢索目錄之目錄名稱的建立方式，必須確保它在伺服器中是唯一的。 因此，伺服器中所有全文檢索目錄之目錄都可以共用相同的路徑。  
  
## <a name="permissions"></a>Permissions  
 呼叫端必須是成員的**db_owner**角色。 根據要求的動作，呼叫端不應被拒絕 ALTER 或 CONTROL 權限 (其中**db_owner**具有) 在目標全文檢索目錄上。  
  
## <a name="examples"></a>範例  
  
### <a name="a-create-a-full-text-catalog"></a>A. 建立全文檢索目錄  
 這個範例會建立一個空白全文檢索目錄， **Cat_Desc**，請在**AdventureWorks2012**資料庫。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'create';  
GO  
```  
  
### <a name="b-to-rebuild-a-full-text-catalog"></a>B. 重建全文檢索目錄  
 這個範例會重建現有的全文檢索目錄， **Cat_Desc**，請在**AdventureWorks2012**資料庫。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'rebuild';  
GO  
```  
  
### <a name="c-start-the-population-of-a-full-text-catalog"></a>C. 開始擴展全文檢索目錄  
 此範例一開始的完整母體擴展**Cat_Desc**類別目錄。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'start_full';  
GO  
```  
  
### <a name="d-stop-the-population-of-a-full-text-catalog"></a>D. 停止擴展全文檢索目錄  
 這個範例會停止擴展**Cat_Desc**類別目錄。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'stop';  
GO  
```  
  
### <a name="e-to-remove-a-full-text-catalog"></a>E. 移除全文檢索目錄  
 這個範例會移除**Cat_Desc**類別目錄。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'drop';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [FULLTEXTCATALOGPROPERTY & #40;TRANSACT-SQL & #41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_database &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)  
  
  
