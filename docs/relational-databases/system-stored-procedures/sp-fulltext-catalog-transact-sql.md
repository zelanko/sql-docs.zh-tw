---
title: sp_fulltext_catalog （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_catalog_TSQL
- sp_fulltext_catalog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_catalog
ms.assetid: e49b98e4-d1f1-42b2-b16f-eb2fc7aa1cf5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4b51e4e38b7587074a39f850c2e56dbd8c09ed6f
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005967"
---
# <a name="sp_fulltext_catalog-transact-sql"></a>sp_fulltext_catalog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  建立和卸除全文檢索目錄，以及啟動和停止目錄的索引動作。 每個資料庫都可以建立多個全文檢索目錄。  
  
> [!IMPORTANT]  
>  @no__t 為0，請改用[CREATE 全文檢索目錄](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)、 [ALTER 全文檢索目錄](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)和[DROP 全文](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)檢索目錄。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_fulltext_catalog [ @ftcat= ] 'fulltext_catalog_name' ,   
     [ @action= ] 'action'   
     [ , [ @path= ] 'root_directory' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @ftcat = ] 'fulltext_catalog_name'` 是全文檢索目錄的名稱。 每個資料庫的目錄名稱都必須是唯一的。 *fulltext_catalog_name*為**sysname**。  
  
`[ @action = ] 'action'` 是要執行的動作。 *action*是**Varchar （20）** ，它可以是下列值之一。  
  
> [!NOTE]  
>  您可以依照需要來建立、卸除和修改全文檢索目錄。 不過，請避免同時變更多個目錄的結構描述。 您可以使用**sp_fulltext_table**預存程式來執行這些動作，這是建議的方法。  
  
|值|描述|  
|-----------|-----------------|  
|**建立**|在檔案系統中建立空白的新全文檢索目錄，並在**sysfulltextcatalogs**中加入相關聯的資料列，其中包含*fulltext_catalog_name*和*root_directory*（如果有的話）值。 *fulltext_catalog_name*在資料庫中必須是唯一的。|  
|**Drop**|卸載*fulltext_catalog_name* ，方法是從檔案系統中移除它，並刪除**sysfulltextcatalogs**中的相關資料列。 如果這個目錄包含一個或多個資料表的索引，這個動作便會失敗。 **sp_fulltext_table**應該執行 '*table_name*'、' drop ' 來卸載目錄中的資料表。<br /><br /> 如果目錄不存在，就會出現錯誤。|  
|**start_incremental**|啟動*fulltext_catalog_name*的累加擴展。 如果目錄不存在，就會出現錯誤。 如果全文檢索索引擴展已在使用中，便會顯示一則警告，但不會進行任何擴展動作。 若為全文檢索索引，則會抓取已變更的資料列，但前提是資料表中有一個**時間戳記**資料行，且已建立全文檢索索引。|  
|**start_full**|啟動*fulltext_catalog_name*的完整擴展。 此時會針對全文檢索索引擷取與這份全文檢索目錄相關聯之每份資料表的每個資料列，即使它們已建立索引也一樣。|  
|**停止**|停止*fulltext_catalog_name*的索引填入。 如果目錄不存在，就會出現錯誤。 如果母體擴展已停止，便不會顯示任何警告。|  
|**Rebuild**|重建*fulltext_catalog_name*。 重建目錄時，會刪除現有的目錄，並就地建立新的目錄。 具有全文檢索索引參考的所有資料表都會與新目錄產生關聯。 重建會重設資料庫系統資料表中的全文檢索中繼資料。<br /><br /> 如果變更追蹤為 OFF，重建並不會重新擴展新建的全文檢索目錄。 在此情況下，若要重新擴展，請使用**start_full**或**start_incremental**動作來執行**sp_fulltext_catalog** 。|  
  
`[ @path = ] 'root_directory'` 是**建立**動作的根目錄（不是完整的實體路徑）。 *root_directory*是**Nvarchar （100）** ，預設值是 Null，表示使用安裝時所指定的預設位置。 這是 Mssql 目錄中的 Ftdata 子目錄;例如，C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\MSSQL\FTData. 指定的根目錄必須在相同電腦的磁碟機中，它不只是磁碟機代號，也不能是相對路徑。 網路磁碟機、卸除式磁碟機、磁碟片及 UNC 路徑都不在支援範圍內。 全文檢索目錄必須建立在與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體相關聯的本機硬碟中。  
  
 只有在**建立***動作*時， **@no__t 1path**才有效。 對於**create** （**stop**， **rebuild**等等）以外的動作， **\@path**必須是 Null 或省略。  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體是叢集中的虛擬伺服器，指定的全文檢索目錄之目錄就必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源所依賴的共用硬碟中。 如果未指定 @path，則預設目錄目錄的位置會位於共用磁片磁碟機上，也就是安裝虛擬伺服器時所指定的目錄中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **Start_full**動作是用來在*fulltext_catalog_name*中建立全文檢索資料的完整快照集。 **Start_incremental**動作是用來只針對資料庫中已變更的資料列重新編制索引。 只有當資料表具有**timestamp**類型的資料行時，才可以套用累加式擴展。 如果全文檢索目錄中的資料表並未包含**timestamp**類型的資料行，則資料表會經歷完整擴展。  
  
 全文檢索目錄和索引資料會儲存在全文檢索目錄之目錄下所建立的檔案中。 如果未指定 **@no__t 3path** ，全文檢索目錄目錄就會建立為 **\@path**或伺服器預設全文檢索目錄目錄中所指定目錄的子目錄。 全文檢索目錄之目錄名稱的建立方式，必須確保它在伺服器中是唯一的。 因此，伺服器中所有全文檢索目錄之目錄都可以共用相同的路徑。  
  
## <a name="permissions"></a>Permissions  
 呼叫端必須是**db_owner**角色的成員。 根據所要求的動作而定，在目標全文檢索目錄上，呼叫端不應被拒絕 ALTER 或 CONTROL 許可權（ **db_owner**所擁有）。  
  
## <a name="examples"></a>範例  
  
### <a name="a-create-a-full-text-catalog"></a>A. 建立全文檢索目錄  
 這個範例會在**AdventureWorks2012**資料庫中建立空的全文檢索目錄**Cat_Desc**。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'create';  
GO  
```  
  
### <a name="b-to-rebuild-a-full-text-catalog"></a>B. 重建全文檢索目錄  
 這個範例會在**AdventureWorks2012**資料庫中重建現有的全文檢索目錄**Cat_Desc**。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'rebuild';  
GO  
```  
  
### <a name="c-start-the-population-of-a-full-text-catalog"></a>C. 開始擴展全文檢索目錄  
 這個範例會開始完整填入**Cat_Desc**目錄。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'start_full';  
GO  
```  
  
### <a name="d-stop-the-population-of-a-full-text-catalog"></a>D. 停止擴展全文檢索目錄  
 這個範例會停止擴展**Cat_Desc**目錄。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'stop';  
GO  
```  
  
### <a name="e-to-remove-a-full-text-catalog"></a>E. 移除全文檢索目錄  
 這個範例會移除**Cat_Desc**目錄。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'drop';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_database &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)  
  
  
