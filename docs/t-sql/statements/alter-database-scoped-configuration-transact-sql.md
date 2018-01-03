---
title: "ALTER DATABASE SCOPED CONFIGURATION (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
caps.latest.revision: "32"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2867f3aff5b8d6d7256d2a9a4ecbe7dcfdccb88c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  這個陳述式可讓數個資料庫設定的設定**個別資料庫**層級。 此陳述式是在[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 這些設定包括：  
  
- 清除程序快取。  
  
- 將主要資料庫的 MAXDOP 參數設定為任意值 (1、2、...，以最適合用於該特定資料庫的值為準)，並且為使用的所有次要資料庫 (例如，用於報告查詢) 設定不同的值 (例如 0)。  
  
- 將與資料庫無關的查詢最佳化工具基數估計模型設定為相容性層級。  
  
- 在資料庫層級啟用或停用參數探測。
  
- 在資料庫層級啟用或停用查詢最佳化。

- 啟用或停用識別快取，在資料庫層級。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ALTER DATABASE SCOPED CONFIGURATION  
{        
     {  [ FOR SECONDARY] SET <set_options>  }    
}  
| CLEAR PROCEDURE_CACHE  
| SET < set_options >
[;]    
  
< set_options > ::=    
{  
    MAXDOP = { <value> | PRIMARY}    
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}    
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}    
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
}  
```  
  
## <a name="arguments"></a>引數  
 
次要資料庫  
 
指定次要資料庫 （所有次要資料庫必須有相同的值） 的設定。  
  
MAXDOP  **=**  {\<值 > |主要}  
**\<值 >**  
  
指定的預設的 MAXDOP 設定，應該用於陳述式。 0 是預設值，並指出將會改為使用伺服器組態。 （除非它已設為 0），會覆寫在資料庫範圍 MAXDOP**的最大平行處理原則程度**sp_configure 設定伺服器層級。 查詢提示仍然可以覆寫資料庫範圍 MAXDOP 以微調需要不同設定的特定查詢。 所有這些設定都受到工作負載群組設定 MAXDOP。   

您可以使用 max degree of parallelism 選項來限制要用於平行計畫執行的處理器數目。 SQL Server 會平行執行計畫的查詢、 索引資料定義語言 (DDL) 作業、 平行插入、 線上改變資料行、 平行 stats collectiion 和靜態和索引鍵集驅動資料指標擴展。
 
若要在執行個體層級中設定這個選項，請參閱[設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 

> [!TIP] 
> 若要完成此工作在查詢層級，將**MAXDOP** [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)。  
  
PRIMARY  
  
只能設定為次要，當資料庫中，在主要伺服器上，並指出組態將會設定為主要。 如果組態中的主要變更，也就是次要資料庫上的值會變更據以而不需要設定次要資料庫的值上明確地。 **主要**是次要資料庫的預設設定。  
  
LEGACY_CARDINALITY_ESTIMATION  **=**  {ON |**OFF** |主要}  

可讓您設定資料庫相容性層級無關之 SQL Server 2012 和舊版查詢最佳化工具基數估計模型。 預設值是**OFF**，查詢最佳化工具基數估計模型會根據資料庫的相容性層級的設定。 將此設定為**ON**相當於啟用[追蹤旗標 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 

> [!TIP] 
> 若要完成此工作在查詢層級，將**QUERYTRACEON** [查詢提示](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入**USE 提示**[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用追蹤旗標。 
  
PRIMARY  
  
此值才有效，當資料庫中主要、 次要和指定的查詢最佳化工具基數估計模型設定所有次要資料庫上會設定為主要的值。 如果查詢最佳化工具基數估計模型的主要組態變更時，次要資料庫上的值會跟著變更。 **主要**是次要資料庫的預設設定。  
  
PARAMETER_SNIFFING  **=**  { **ON** |關閉 |主要}  

啟用或停用[參數探測](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)。 預設值是 ON。 這與 [追蹤旗標 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)相同。   

> [!TIP] 
> 若要完成此工作在查詢層級，請參閱**OPTIMIZE FOR UNKNOWN** [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)。 從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級**USE 提示**[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)也會提供。 
  
PRIMARY  
  
此值才有效，當資料庫中主要、 次要資料庫上，並指定所有次要資料庫上的這個設定的值將會針對主要設定的值。 如果在主要伺服器上使用的組態[參數探測](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)變更時，變更次要資料庫上的值會隨之而不需要設定次要資料庫的值上明確地。 這是次要資料庫的預設設定。  
  
QUERY_OPTIMIZER_HOTFIXES  **=**  {ON |**OFF** |主要}  

啟用或停用查詢最佳化 hotfix，不論資料庫的相容性層級。 預設值是**OFF**，讓停用查詢最佳化 hotfix，發行後的特定版本引進的高可用的相容性層級 (post RTM)。 將此設定為**ON**相當於啟用[追蹤旗標 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。   

> [!TIP] 
> 若要完成此工作在查詢層級，將**QUERYTRACEON** [查詢提示](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用追蹤旗標。  
  
PRIMARY  
  
此值才有效，當資料庫中主要、 次要資料庫上，並指定所有次要資料庫上的這個設定的值將會針對主要設定的值。 如果組態中的主要變更，也就是次要資料庫上的值會變更據以而不需要設定次要資料庫的值上明確地。 這是次要資料庫的預設設定。  
  
清除 PROCEDURE_CACHE  

清除程序 （計劃） 快取中的資料庫。 這可以同時在主要和次要資料庫上執行。  

IDENTITY_CACHE  **=**  { **ON** |OFF}  

**適用於**:[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

啟用或停用識別快取，在資料庫層級。 預設值是**ON**。 識別快取用來改善插入具有識別資料行的資料表上的效能。 若要避免伺服器意外重新啟動或容錯移轉至次要伺服器識別資料行值的間距，停用 IDENTITY_CACHE 選項。 這個選項是類似現有[追蹤旗標 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)，不同之處在於它可在資料庫層級，而不是只能在伺服器層級設定。   

> [!NOTE] 
> 這個選項只能設定為主要。 如需詳細資訊，請參閱[識別資料行](create-table-transact-sql-identity-property.md)。  

##  <a name="Permissions"></a> 權限  
 需要改變任何資料庫範圍組態   
在資料庫中。 控制資料庫上的權限的使用者可以授與此權限。  
  
## <a name="general-remarks"></a>一般備註  
 雖然您可以設定次要資料庫具有從其主要的不同範圍的組態設定，所有次要資料庫會使用相同的設定。 不同的設定不能設定為個別的次要。  
  
 執行此陳述式將會清除在目前資料庫中，這表示所有查詢將會都需要重新編譯程序快取。  
  
 3 部分名稱查詢，查詢目前的資料庫連接的設定將會接受的而不會編譯目前的資料庫內容中的 SQL 模組 （例如程序、 函數和觸發程序），因此將使用的選項所在的資料庫。  
  
 ALTER_DATABASE_SCOPED_CONFIGURATION 事件會新增為可用來引發 DDL 觸發程序的 DDL 事件。 這是 ALTER_DATABASE_EVENTS 觸發程序群組的子系。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
**MAXDOP**  
  
 細微的設定可以覆寫的全域項目，以及該資源管理員可以限制在所有其他的 MAXDOP 設定。  MAXDOP 設定的邏輯如下所示：  
  
-   查詢提示會覆寫 sp_configure 和資料庫範圍設定。 如果 MAXDOP 設定工作負載群組的資源群組：  
  
    -   如果查詢提示設定為 0 就會覆寫設定資源管理員。  
  
    -   如果查詢提示不是 0，就會受限於設定資源管理員。  
  
-   除非查詢提示設定 （除非它是 0） 的資料庫範圍覆寫 sp_configure 設定和設定資源管理員會受限於。  
  
-   資源管理員設定會覆寫 sp_configure 設定。  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 啟用查詢最佳化工具 hotfix 的舊版查詢最佳化工具使用 QUERYTRACEON 提示時，將查詢提示與資料庫範圍組態設定，這就表示的選項會套用如果是已啟用，OR 條件。  
  
**具有 GeoDR**  
  
 可讀取的次要資料庫，例如 Alwayson 可用性群組和 GeoReplication，使用第二個值，藉由檢查資料庫狀態。 雖然我們不在容錯移轉時重新編譯，而且技術上新的主要查詢所使用的次要的設定值，這個概念是主要與次要資料庫之間的設定將只會改變時的工作負載是不同結果，因此快取的查詢而新的查詢將會挑選新的設定，也就是他們使用的最佳的設定。  
  
**DacFx**  
  
 由於 ALTER DATABASE SCOPED CONFIGURATION 是 Azure SQL Database 和 SQL Server 2016 會影響資料庫結構描述中的新功能，將匯出的結構描述 （不論有無資料） 將無法匯入至較舊版本的 SQL Server 例如[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 <c2 > [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)] 。 例如，若要匯出[DACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3)或[BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4)從[!INCLUDE[ssSDS](../../includes/sssds-md.md)]或[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]使用這項新功能的資料庫將無法匯入到下層伺服器。  
  
## <a name="metadata"></a>中繼資料  

[Sys.database_scoped_configurations &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)系統檢視表提供在資料庫中已設定領域的組態資訊。 資料庫範圍組態選項才會顯示在 sys.database_scoped_configurations 不覆寫，以整個伺服器的預設設定。 [Sys.configurations &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)系統檢視表只會顯示整個伺服器設定。  
  
## <a name="examples"></a>範例  
這些範例示範如何使用 ALTER DATABASE SCOPED CONFIGURATION  
  
### <a name="a-grant-permission"></a>A. 授與權限  

此範例中，授與權限，才能執行 ALTER DATABASE SCOPED CONFIGURATION     
使用者 [Joe]。  
  
```sql  
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;  
```  
  
### <a name="b-set-maxdop"></a>B. 設定 MAXDOP  

此範例會設定 MAXDOP = 1 適用於主要資料庫和 MAXDOP = 4 的地理複寫案例中，次要資料庫。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=4 ;  
```  
  
此範例會設定次要資料庫的 MAXDOP 必須相同，因為設定的主要資料庫在地理複寫案例。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>C. 設定 LEGACY_CARDINALITY_ESTIMATION  

此範例的地理複寫案例中，次要資料庫設定為 ON LEGACY_CARDINALITY_ESTIMATION。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
這個範例會設定 LEGACY_CARDINALITY_ESTIMATION 次要資料庫，所以其主要資料庫中的地理複寫案例。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=PRIMARY ;  
```  
  
### <a name="d-set-parametersniffing"></a>D. 設定 PARAMETER_SNIFFING  

此範例的地理複寫案例的主要資料庫設定為 OFF PARAMETER_SNIFFING。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING =OFF ;  
```  
  
此範例的地理複寫案例的主要資料庫設定為 OFF PARAMETER_SNIFFING。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=OFF ;  
```  
  
這個範例 PARAMETER_SNIFFING 次要資料庫的設定，所以主要資料庫上   
在地理複寫的案例。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>E. 設定 QUERY_OPTIMIZER_HOTFIXES  

QUERY_OPTIMIZER_HOTFIXES 設為 ON，主要資料庫   
在地理複寫的案例。  

```sql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>F. 清除程序快取  

這個範例會清除程序快取 （僅適用於主要資料庫可能的話）。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>G. 設定 IDENTITY_CACHE

**適用於**:[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]（功能處於公開預覽狀態） 

這個範例會停用識別快取。

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

## <a name="additional-resources"></a>其他資源

### <a name="maxdop-resources"></a>MAXDOP 資源 
* [平行處理原則的程度](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [建議和指導方針 SQL Server 中的"max degree of parallelism"組態選項](https://support.microsoft.com/en-us/kb/2806535) 

### <a name="legacycardinalityestimation-resources"></a>LEGACY_CARDINALITY_ESTIMATION 資源    
* [基數估計 (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) (使用 SQL Server 2014 基數估算程式最佳化您的查詢計劃)

### <a name="parametersniffing-resources"></a>PARAMETER_SNIFFING 資源    
* [參數探測](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* [「 我想也參數 ！ 」](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/)

### <a name="queryoptimizerhotfixes-resources"></a>QUERY_OPTIMIZER_HOTFIXES 資源    
* [追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [SQL Server 查詢最佳化工具 hotfix 追蹤旗標 4199 服務模型](https://support.microsoft.com/en-us/kb/974006)

## <a name="more-information"></a>詳細資訊  
 [sys.database_scoped_configurations &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [資料庫和檔案目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server &#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sys.configurations &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
  
  
