---
title: DROP SENSITIVITY CLASSIFICATION (Transact-SQL) | Microsoft Docs
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
- DROP SENSITIVITY CLASSIFICATION
- DROP_SENSITIVITY_CLASSIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SENSITIVITY CLASSIFICATION statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5e873944e68a05b29ed865572202e7e2b4438d76
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816894"
---
# <a name="drop-sensitivity-classification-transact-sql"></a>DROP SENSITIVITY CLASSIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

卸除來自至一或多個資料庫資料行的敏感度分類中繼資料。

## <a name="syntax"></a>語法

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    <object_name> [, ...n ]

<object_name> ::=
{
    [schema_name.]table_name.column_name
}
```  

## <a name="arguments"></a>引數  

*object_name* ([schema_name.]table_name.column_name)

是要移除其分類的資料庫資料行名稱。 目前只支援資料行分類。
    - *schema_name* (選用) - 是分類的資料行所屬的結構描述名稱。
    - *table_name* - 是分類的資料行所屬的資料表名稱。
    - *column_name* - 是要卸除分類的資料行名稱。

## <a name="remarks"></a>Remarks  

- 多個物件分類可利用單一 ‘DROP SENSITIVITY CLASSIFICTION’ 陳述式來卸除。

## <a name="permissions"></a>[權限]  

需要 ALTER ANY SENSITIVITY CLASSIFICATION 權限。 ALTER ANY SENSITIVITY CLASSIFACTION 是由資料庫權限 ALTER，或由伺服器權限 CONTROL SERVER 默許。


## <a name="examples"></a>範例  


### <a name="a-dropping-classification-from-a-single-column"></a>A. 卸除單一資料行的分類

下列範例會從資料欄 `dbo.sales.price` 中移除分類。  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price
```

### <a name="b-dropping-classification-from-multiple-columns"></a>B. 卸除多個資料行的分類

下列範例會從資料欄 `dbo.sales.price`、`dbo.sales.discount` 及 `SalesLT.Customer.Phone` 中移除分類。  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price, dbo.sales.discount, SalesLT.Customer.Phone  
```

## <a name="see-also"></a>另請參閱  

[ADD SENSITIVITY CLASSIFICTION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[sys.sensitivity_classifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)

[開始使用 SQL 資訊保護](http://aka.ms/sqlip)
