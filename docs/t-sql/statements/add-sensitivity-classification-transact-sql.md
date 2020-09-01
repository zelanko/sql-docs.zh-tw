---
description: ADD SENSITIVITY CLASSIFICATION (Transact-SQL)
title: ADD SENSITIVITY CLASSIFICATION (Transact-SQL)
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
author: DavidTrigano
ms.author: datrigan
ms.reviewer: vanto
f1_keywords:
- ADD SENSITIVITY CLASSIFICATION
- ADD_SENSITIVITY_CLASSIFICATION
helpviewer_keywords:
- ADD SENSITIVITY CLASSIFICATION statement
- add labels
- adding labels
- adding labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
- rank
ms.custom: ''
ms.date: 06/10/2020
monikerRange: " >= sql-server-linux-ver15 || >= sql-server-ver15 || = azuresqldb-current || = sqlallproducts-allversions"
ms.openlocfilehash: 641896fb407beabdedbd30d98cc8d94d16d31efe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991876"
---
# <a name="add-sensitivity-classification-transact-sql"></a>ADD SENSITIVITY CLASSIFICATION (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

將有關敏感度分類的中繼資料新增至一或多個資料庫資料行。 分類可包含敏感度標籤和資訊類型。

若是 SQL Server，這是在 SQL Server 2019 中導入的。

將資料庫環境中的機密資料分類，可協助達到擴充可見度和更佳的防護。 [開始使用 SQL 資訊保護](https://aka.ms/sqlip)中可以找到其他資訊

## <a name="syntax"></a>語法

```syntaxsql
    ADD SENSITIVITY CLASSIFICATION TO
    <object_name> [, ...n ]
    WITH ( <sensitivity_option> [, ...n ] )

<object_name> ::=
{
    [schema_name.]table_name.column_name
}

<sensitivity_option> ::=  
{
    LABEL = string |
    LABEL_ID = guidOrString |
    INFORMATION_TYPE = string |
    INFORMATION_TYPE_ID = guidOrString |
    RANK = NONE | LOW | MEDIUM | HIGH | CRITICAL
}
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數  

*object_name* ([schema_name.]table_name.column_name)

是要分類的資料庫資料行名稱。 目前只支援資料行分類。
    - *schema_name* (選用) - 是分類的資料行所屬的結構描述名稱。
    - *table_name* - 是分類的資料行所屬的資料表名稱。
    - *column_name* - 是所分類的資料行名稱。

*LABEL*

是人類看得懂的敏感度標籤名稱。 敏感度標籤代表資料庫資料行中所儲存資料的敏感度。

*LABEL_ID*

是與敏感度標籤相關聯的識別碼。 集中式資訊保護平台常用此來唯一識別系統中的標籤。

*INFORMATION_TYPE*

是人類看得懂的資訊類型名稱。 資訊類型是用來描述資料庫資料行中所儲存的資料類型。

*INFORMATION_TYPE_ID*

是與資訊類型相關聯的識別碼。 集中式資訊保護平台常用此來唯一識別系統中的資訊類型。

*RANK*

為識別碼，其以定義敏感度等級的一組預先定義值為基礎。 由其他服務 (例如進階威脅防護) 用於根據其等級偵測異常。

## <a name="remarks"></a>備註  

- 單一物件只能新增一個分類。 將分類新增至已分類的物件會覆寫現有的分類。
- 多個物件可使用單一 `ADD SENSITIVITY CLASSIFICATION` 陳述式來分類。
- 系統檢視 [sys.sensitivity_classifications](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md) 可用來擷取資料庫的敏感度分類資訊。

## <a name="permissions"></a>權限

需要 ALTER ANY SENSITIVITY CLASSIFICATION 權限。 ALTER ANY SENSITIVITY CLASSIFICATION 是由資料庫權限 ALTER，或由伺服器權限 CONTROL SERVER 所隱含。

## <a name="examples"></a>範例  

### <a name="a-classifying-two-columns"></a>A. 將兩個資料行分類

下列範例以 **Highly Confidential** 敏感度標籤、**Critical** 等級及 **Financial** 資訊類型來分類 **dbo.sales.price** 與 **dbo.sales.discount** 資料行。

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.sales.price, dbo.sales.discount
    WITH ( LABEL='Highly Confidential', INFORMATION_TYPE='Financial', RANK=CRITICAL )
```  

### <a name="b-classifying-only-a-label"></a>B. 僅分類標籤

下列範例以**Confidential** 標籤與標籤識別碼 **643f7acd-776a-438d-890c-79c3f2a520d6**，將**dbo.customer.comments** 資料行分類。 此資料行的資訊類型並未分類。

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.customer.comments
    WITH ( LABEL='Confidential', LABEL_ID='643f7acd-776a-438d-890c-79c3f2a520d6' )
```  

## <a name="see-also"></a>另請參閱

- [DROP SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)
- [sys.sensitivity_classifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)
- [權限 (資料庫引擎)](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine)
- [開始使用 SQL 資訊保護](https://aka.ms/sqlip)
