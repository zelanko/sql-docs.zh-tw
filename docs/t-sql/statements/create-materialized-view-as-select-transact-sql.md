---
title: CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: data-warehouse
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: e8acc3ef73c51ccbbf195f9d18dc5f12d661931f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75226738"
---
# <a name="create-materialized-view-as-select-transact-sql"></a>CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL)  

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

此文章說明 Azure SQL 資料倉儲中用於開發解決方案的 CREATE MATERIALIZED VIEW AS SELECT T-SQL 陳述式。 此文章也提供程式碼範例。

具體化檢視會保存從檢視定義查詢傳回的資料，並在底層資料表中的資料變更時自動取得更新。   它可以改進複雜查詢 (通常是具有聯結與會總的查詢) 的效能，同時提供簡單的維護作業。   使用其執行計畫的自動比對功能，不需要在查詢中參考具體化檢視，最佳化工具就能考慮要替代的檢視。  這可讓資料工程師將具體化檢視實作為改進查詢回應時間的機制，而不需要變更查詢。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE MATERIALIZED VIEW [ schema_name. ] materialized_view_name
    WITH (  
      <distribution_option>
    )
    AS <select_statement>
[;]

<distribution_option> ::=
    {  
        DISTRIBUTION = HASH ( distribution_column_name )  
      | DISTRIBUTION = ROUND_ROBIN  
    }

<select_statement> ::=
    SELECT select_criteria
```  
  
## <a name="arguments"></a>引數

*schema_name*     
 這是檢視所屬的結構描述名稱。  
  
*materialized_view_name*   
這是檢視的名稱。 檢視名稱必須遵照識別碼的規則。 指定檢視擁有者名稱則是選擇性的。  

*分佈選項*     
只支援 HASH 與 ROUND_ROBIN 分佈。

*select_statement*   
具體化檢視定義中的 SELECT 清單必須符合下列兩個條件的至少其中一個：
- SELECT 清單包含彙總函式。
- GROUP BY 用於具體化檢視定義中，而且 GROUP BY 中的所有資料行都包括在 SELECT 清單中。  GROUP BY 子句中最多可以使用 32 個資料行。

具體化檢視定義的 SELECT 清單中需要彙總函式。  支援的彙總包括 MAX、MIN、AVG、COUNT、COUNT_BIG、SUM、VAR、STDEV。

當在具體化檢視定義的 SELECT 清單中使用 MIN/MAX 彙總時，必須符合下列需求：
 
- 需要 FOR_APPEND。  例如：
  ```sql 
  CREATE MATERIALIZED VIEW mv_test2  
  WITH (distribution = hash(i_category_id), FOR_APPEND)  
  AS
  SELECT MAX(i.i_rec_start_date) as max_i_rec_start_date, MIN(i.i_rec_end_date) as min_i_rec_end_date, i.i_item_sk, i.i_item_id, i.i_category_id
  FROM syntheticworkload.item i  
  GROUP BY i.i_item_sk, i.i_item_id, i.i_category_id
  ```

- 當參考的基底資料表中發生 UPDATE 或 DELETE 時，將停用具體化檢視。  此限制不適用於 INSERT。  若要重新啟用具體化檢視，請搭配 REBUILD 執行 ALTER MATERIALIZED。
  
## <a name="remarks"></a>備註

Azure 資料倉儲中的具體化檢視非常類似 SQL Server 中的索引檢視表。  它的限制幾乎與索引檢視表相同 (請參閱[建立索引檢視表](/sql/relational-databases/views/create-indexed-views)以取得詳資訊)，不過具體化檢視支援彙總函式。   具體化檢視有其他考量事項。  
 
只有具體化檢視才支援 CLUSTERED COLUMNSTORE INDEX。 

具體化檢視無法參考其他檢視。  
 
具體化檢視可在資料分割資料表上建立。  具體化檢視中參考的資料表上支援 SPLIT/MERGE 作業。  具體化檢視中參考的資料表上不支援 SWITCH。 若嘗試，使用者將會看到錯誤 `Msg 106104, Level 16, State 1, Line 9`
 
具體化檢視中參考的資料表上不支援 ALTER TABLE SWITCH。 在使用 ALTER TABLE SWITCH 之前停用或捨棄具體化檢視。 在下列案例中，具體化檢視建立要求必須將新資料行新增到具體化檢視：

|狀況|新資料行必須新增到具體化檢視|註解|  
|-----------------|---------------|-----------------|
|在具體化檢視定義的 SELECT 清單中，遺漏 COUNT_BIG ()| COUNT_BIG (*) |已由具體化檢視建立自動新增。  使用者不必採取任何動作。|
|SUM(a) 是由使用者在具體化檢視定義的 SELECT 清單中指定的，而且 ‘a’ 是可為 Null 的運算式 |COUNT_BIG (a) |使用者必須手動在具體化檢視定義中新增運算式 ‘a’。|
|AVG(a) 是由使用者在 ‘a’ 是運算式之具體化檢視定義的 SELECT 清單中指定的。|SUM(a)、COUNT_BIG(a)|已由具體化檢視建立自動新增。  使用者不必採取任何動作。|
|STDEV(a) 是由使用者在 ‘a’ 是運算式之具體化檢視定義的 SELECT 清單中指定的。|SUM(a)、COUNT_BIG(a)、SUM(square(a))|已由具體化檢視建立自動新增。  使用者不必採取任何動作。 |
| | | |

一旦建立，具體化檢視在 SQL Server Management Studio 內 Azure SQL 資料倉儲執行個體的檢視資料夾下就是可見的。

使用者可以執行 [SP_SPACEUSED](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql?view=azure-sqldw-latest) 與 [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql?view=azure-sqldw-latest) 來判斷具體化檢視取用的空間。  

具體化檢視可透過 DROP VIEW 來捨棄。  您可以使用 ALTER MATERIALIZED VIEW 來停用或重建具體化檢視。   

SQL Server Management Studio 中的 EXPLAIN 計畫與圖形化預估執行計畫可以顯示具體化檢視是否由查詢最佳化工具考量為查詢執行使用。 SQL Server Management Studio 中的 與圖形化預估執行計畫可以顯示具體化檢視是否由查詢最佳化工具考量為查詢執行使用。

若要判斷 SQL 陳述式是否可從新的具體化檢視獲益，請搭配 `WITH_RECOMMENDATIONS` 執行 `EXPLAIN` 命令。  如需詳細資訊，請參閱 [EXPLAIN (Transact-SQL)](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)。

## <a name="permissions"></a>權限

至少必須有資料庫中的 CREATE VIEW 權限，以及正在建立之檢視表所在之結構描述的 ALTER 權限。 
  
## <a name="see-also"></a>另請參閱

[使用具體化檢視進行效能調整](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)      
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL 資料倉儲中支援的系統檢視](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL 資料倉儲中支援的 T-SQL 陳述式](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
