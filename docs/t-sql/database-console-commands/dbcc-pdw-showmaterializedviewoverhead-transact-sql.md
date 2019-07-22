---
title: DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: XiaoyuL-Preview
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 626fed3686ab85f4d24a353edba5f6bb9c4d174e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117745"
---
# <a name="dbcc-pdwshowmaterializedviewoverhead-transact-sql-preview"></a>DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD (Transact-SQL) (預覽)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

在針對 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 中具體化檢視保存的基底資料表中顯示增量變更。 額外負荷率的計算方式為 TOTAL_ROWS / MAX (1, BASE_VIEW_ROWS)。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法

```
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ( " [ schema_name .] materialized_view_name  " )
[;]
```
  
## <a name="arguments"></a>引數

 *schema_name*     
 這是檢視所屬的結構描述名稱。

*materialized_view_name*   
是具體化檢視的名稱。

## <a name="remarks"></a>Remarks

當修改具體化檢視之定義中的底層資料表時，會針對具體化檢視維持該基底資料表中的所有增量變更。  從具體化檢視選取包括掃描具體化檢視的叢集資料行從放區結構，以及套用這些增量變更。   若保留的增量變更數目太高，選取效能將會變差。  使用者可以重建具體化檢視以建立叢集資料行存放區結構並在基底資料表中彙總所有增量變更。
  
## <a name="permissions"></a>權限  
  
需要 VIEW DATABASE STATE 權限。  

## <a name="example"></a>範例  

此範例會傳回用於具體化檢視的差異空間。

```sql
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ( "dbo.MyIndexedView" )
```

輸出：

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|1234|1|3 |3.0 |

</br>

|OBJECT_ID |BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|
|4567|0|0|0.0|

</br>

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|
|789|0|2|2.0|

## <a name="see-also"></a>另請參閱

[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL 資料倉儲中支援的系統檢視](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL 資料倉儲中支援的 T-SQL 陳述式](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)