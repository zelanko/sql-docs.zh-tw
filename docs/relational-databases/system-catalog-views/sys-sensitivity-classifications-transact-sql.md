---
description: sys.sensitivity_classifications (Transact-SQL)
title: sys. sensitivity_classifications (Transact-sql) |Microsoft Docs
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
monikerRange: '>= sql-server-ver15 || = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5f1dfa43dba7848732e57acf4abf8cfa915be255
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475299"
---
# <a name="syssensitivity_classifications-transact-sql"></a>sys.sensitivity_classifications (Transact-SQL)
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

針對資料庫中的每個分類專案，各傳回一個資料列。

|資料行名稱|資料類型|描述|
|-----------------|---------------|-----------------|  
|**class**|**int**|識別存在分類之專案的類別。 一律會有代表資料行的值 1 () |  
|**class_desc**|**Varchar (16) **|存在分類之專案類別的描述。 一律會有值 *OBJECT_OR_COLUMN*|  
|**major_id**|**int**|表示包含已分類資料行之資料表的識別碼，對應于 sys. all_objects。 object_id|  
|**minor_id**|**int**|代表存在分類的資料行識別碼，對應于 sys. all_columns。 column_id|   
|**label**|**sysname**|指派給敏感度分類 (人類可讀取) 的標籤|  
|**label_id**|**sysname**|與標籤相關聯的識別碼，可供資訊保護系統（例如 Azure 資訊保護 (AIP）使用) |  
|**information_type**|**sysname**| (為敏感度分類指派的人類可讀取) 資訊類型|  
|**information_type_id**|**sysname**|與資訊類型相關聯的識別碼，可供資訊保護系統（例如 Azure 資訊保護 (AIP）使用) |  
|**排名**|**int**|次序的數值： <br><br>0代表無<br>10表示低<br>20代表中型<br>高達30<br>適用于重大的40| 
|**rank_desc**|**sysname**|順位的文字標記法：  <br><br>無、低、中、高、重大|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>備註  

- 此視圖可讓您查看資料庫的分類狀態。 它可用來管理資料庫分類，以及用來產生報表。
- 目前只支援資料庫資料行的分類。
 
## <a name="examples"></a>範例

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. 列出所有已分類的資料行及其對應的分類

下列範例會傳回資料表，其中列出資料庫中每個已分類資料行的資料表名稱、資料行名稱、標籤、標籤識別碼、資訊類型、資訊類型識別碼、排名和順位描述。

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
 需要 **VIEW ANY 敏感度分類** 許可權。 
 
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  

## <a name="see-also"></a>另請參閱  

[ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[開始使用 SQL 資訊保護](https://aka.ms/sqlip)
