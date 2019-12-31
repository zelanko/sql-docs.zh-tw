---
title: sys.databases sensitivity_classifications （Transact-sql） |Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.author: mibar
author: barmichal
f1_keywords:
- 'sys.sensitivity_classifications '
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sensitivity_classifications statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
- rank
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 376438a45d6b104cbf4e66dbdf8e5542cf3fd2c2
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542056"
---
# <a name="syssensitivity_classifications-transact-sql"></a>sys.sensitivity_classifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

針對資料庫中的每個分類專案，各傳回一個資料列。

|資料行名稱|資料類型|描述|
|-----------------|---------------|-----------------|  
|**class**|**int**|識別分類所在專案的類別。 一定會有值1（表示資料行）|  
|**class_desc**|**Varchar （16）**|分類所在專案的類別描述。 一定會有值*OBJECT_OR_COLUMN*|  
|**major_id**|**int**|表示包含分類資料行之資料表的識別碼，其對應于 sys.databases all_objects。 object_id|  
|**minor_id**|**int**|代表分類所在之資料行的識別碼，其對應于 sys.databases. all_columns。 column_id|   
|**標誌**|**sysname**|指派給敏感度分類的標籤（人類可讀取）|  
|**label_id**|**sysname**|與標籤相關聯的識別碼，可供資訊保護系統（例如 Azure 資訊保護（AIP））使用|  
|**information_type**|**sysname**|指派給敏感度分類的資訊類型（人類可讀取）|  
|**information_type_id**|**sysname**|與資訊類型相關聯的識別碼，可供資訊保護系統（例如 Azure 資訊保護（AIP））使用|  
|**等級**|**int**|次序的數值： <br><br>0代表無<br>10適用于低<br>20適用于中<br>30（高）<br>適用于重大的40| 
|**rank_desc**|**sysname**|順位的文字表示：  <br><br>NONE、LOW、MEDIUM、HIGH、CRITICAL|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>備註  

- 這個視圖可讓您看到資料庫的分類狀態。 它可以用來管理資料庫分類，以及產生報表。
- 目前僅支援資料庫資料行的分類。
 
## <a name="examples"></a>範例

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. 列出所有分類的資料行及其對應的分類

下列範例會傳回一個資料表，其中列出資料庫中每個分類資料行的資料表名稱、資料行名稱、標籤、標籤識別碼、資訊類型、資訊類型識別碼。

> [!NOTE]
> 標籤是 Azure SQL 資料倉儲的關鍵字。

```sql
SELECT
    SCHEMA_NAME(sys.all_objects.schema_id) as SchemaName,
    sys.all_objects.name AS [TableName], sys.all_columns.name As [ColumnName],
    [Label], [Label_ID], [Information_Type], [Information_Type_ID], [Rank], [Rank_Desc]
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="permissions"></a>權限  
 需要**VIEW ANY 敏感度分類**許可權。 
 
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]如需詳細資訊，請參閱[中繼資料可見度](../../relational-databases/security/metadata-visibility-configuration.md)設定。  

## <a name="see-also"></a>另請參閱  

[加入敏感度分類（Transact-sql）](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP 敏感度分類（Transact-sql）](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[SQL 資訊保護入門](https://aka.ms/sqlip)
