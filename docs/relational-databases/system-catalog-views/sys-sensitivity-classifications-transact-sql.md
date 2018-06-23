---
title: sys.sensitivity_classifications (TRANSACT-SQL) |Microsoft 文件
ms.date: 06/17/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology: t-sql
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d0adbbeb82c06d6a44f3a7439bcbf479d7358401
ms.sourcegitcommit: 70882926439a63ab9d812809429c63040eb9a41b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36262881"
---
# <a name="syssensitivityclassifications-transact-sql"></a>sys.sensitivity_classifications (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

傳回資料庫中的每個分類項目的資料列。

|資料行名稱|資料類型|描述|
|-----------------|---------------|-----------------|  
|**class**|**int**|識別有該分類的項目類別|  
|**class_desc**|**varchar （16)**|有該分類的項目類別的描述|  
|**major_id**|**int**|有該分類的項目識別碼。 < b \>< b\>如果 class 是 0，則 major_id 一律為 0。<br>如果 class 是 1、2 或 7，則 major_id 就是 object_id。|  
|**minor_id**|**int**|次要有該分類，根據其類別加以解譯的項目 ID。<br><br>如果類別 = 1，minor_id 就是 column_id (如果資料行)，否則就是 0 (如果物件)。<br>如果 class = 2，minor_id 就是 parameter_id。<br>如果類別 = 7，minor_id 就是 index_id。 |  
|**label**|**sysname**|指派敏感度分類的標籤 （可讀取）|  
|**label_id**|**sysname**|相關聯的標籤，可供 Azure 資訊保護 (AIP) 等資訊保護系統識別碼|  
|**information_type**|**sysname**|指派敏感度分類的資訊類型 （可讀取）|  
|**information_type_id**|**sysname**|資訊類型，可以使用資訊保護系統例如 Azure 資訊保護 (AIP) 與相關聯識別碼|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>備註  

- 此檢視會提供可見性分類資料庫的狀態。 它可以用於管理資料庫分類，以及產生報表。
- 支援的資料庫資料行的目前只支援分類。 因此：
    - **類別**-永遠會將值 1 （表示資料行）
    - **class_desc** -永遠會值*OBJECT_OR_COLUMN*
    - **則 major_id 就**-代表 sys.all_objects.object_id 與對應的資料表，內含分類資料行，識別碼
    - **minor_id** -代表在其有該分類，與 sys.all_columns.column_id 對應資料行的識別碼

## <a name="examples"></a>範例

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. 列出所有分類資料行和其對應的分類

一個資料表列出的資料表名稱、 資料行名稱、 標籤，下列範例會傳回加上標籤識別碼、 輸入的資訊，每個分類資料行在資料庫中的資訊類型識別碼。

```sql
SELECT
    sys.all_objects.name AS TableName, sys.all_columns.name As ColumnName,
    Label, Label_ID, Information_Type, Information_Type_ID
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="see-also"></a>另請參閱  

[新增敏感度 CLASSIFICTION (TRANSACT-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[卸除敏感度 CLASSIFICTION (TRANSACT-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[使用 SQL Information Protection 快速入門](http://aka.ms/sqlip)
