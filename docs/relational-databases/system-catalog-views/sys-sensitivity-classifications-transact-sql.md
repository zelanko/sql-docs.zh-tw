---
title: sys.sensitivity_classifications (TRANSACT-SQL) |Microsoft Docs
ms.date: 06/17/2018
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
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
ms.openlocfilehash: 0fb7b7719ce53fe4f20863cb3f44c9483bc6b472
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660347"
---
# <a name="syssensitivityclassifications-transact-sql"></a>sys.sensitivity_classifications & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

傳回資料庫中的每個分類的項目資料列。

|資料行名稱|資料類型|描述|
|-----------------|---------------|-----------------|  
|**class**|**int**|識別類別的分類所在處的項目|  
|**class_desc**|**varchar(16)**|類別的分類所在處的項目描述|  
|**major_id**|**int**|分類所在處的項目識別碼。 < b \>< b\>如果 class 是 0，則 major_id 一律為 0。<br>如果 class 是 1、2 或 7，則 major_id 就是 object_id。|  
|**minor_id**|**int**|第二個項目 ID 的分類所在處，根據其類別加以解譯。<br><br>如果類別 = 1，minor_id 是 column_id (如果資料行)，否則就是 0 (如果物件)。<br>如果 class = 2，minor_id 就是 parameter_id。<br>如果類別 = 7，7,minor_id 就是 index_id。 |  
|**label**|**sysname**|指派敏感度分類的標籤 （可讀取）|  
|**label_id**|**sysname**|相關聯的標籤，可供 Azure 資訊保護 (AIP) 等資訊保護系統識別碼|  
|**information_type**|**sysname**|指派敏感度分類的資訊類型 （可讀取）|  
|**information_type_id**|**sysname**|資訊類型，可用的資訊保護系統等 Azure 資訊保護 (AIP) 相關聯識別碼|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>備註  

- 此檢視會提供資料庫分類狀態的可視性。 它可用來管理資料庫分類，以及產生報表。
- 支援的資料庫資料行的目前只支援分類。 因此：
    - **類別**-永遠會將值 1 （代表的資料行）
    - **class_desc** -一律會有值*OBJECT_OR_COLUMN*
    - **則 major_id 就**-代表與 sys.all_objects.object_id 對應包含分類的資料行，資料表的識別碼
    - **minor_id** -代表分類所在處，sys.all_columns.column_id 與對應的資料行的識別碼

## <a name="examples"></a>範例

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. 列出所有分類資料行和其對應的分類

下列範例傳回的資料表，其中列出的資料表名稱、 資料行名稱、 標籤，標籤識別碼、 資訊類型，每個已分類資料行在資料庫中的資訊類型識別碼。

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

[ADD SENSITIVITY CLASSIFICTION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP SENSITIVITY CLASSIFICTION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[開始使用 SQL 資訊保護](https://aka.ms/sqlip)
