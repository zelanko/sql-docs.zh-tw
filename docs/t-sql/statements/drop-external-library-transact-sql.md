---
description: DROP EXTERNAL LIBRARY (Transact-SQL)
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 98ce649f2b0c2f1d9788deddecfa5294c0325230
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2020
ms.locfileid: "91378473"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

刪除現有的套件程式庫。 支援的外部執行階段 (例如 R、Python 或 Java) 會使用套件程式庫。

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||sqlallproducts-allversions"
> [!NOTE]
> 在 SQL Server 2017 中，支援 R 語言和 Windows 平台。 SQL Server 2019 及更新版本支援 Windows 和 Linux 平台上的 R、Python 和 Java。
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
> [!NOTE]
> 在 Azure SQL 受控執行個體中，只支援 R 和 Python 語言。
::: moniker-end

## <a name="syntax"></a>語法

```syntaxsql
DROP EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ];
```

### <a name="arguments"></a>引數

**library_name**

指定現有套件程式庫的名稱。

程式庫的範圍限制為使用者。 程式庫名稱在特定使用者或擁有者的內容中必須是唯一的。

**owner_name**

指定擁有外部程式庫的使用者或角色名稱。

資料庫擁有者可以刪除其他使用者建立的程式庫。

## <a name="permissions"></a>權限

若要刪除程式庫，需要 ALTER ANY EXTERNAL LIBRARY 權限。 根據預設，任何資料庫擁有者或物件的擁有者，也可刪除外部程式庫。

### <a name="return-values"></a>傳回值

如果陳述式執行成功，會傳回參考訊息。

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>備註

不同於 SQL Server 中的其他 `DROP` 陳述式，此陳述式支援指定選擇性授權子句。 這可讓 **db_owner** 角色中的 **dbo** 或使用者卸除資料庫中由一般使用者上傳的套件資料庫。

SQL 執行個體中已預先安裝一些套件 (稱為「系統套件」)。 使用者無法新增、更新或移除系統套件。

## <a name="examples"></a>範例

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
將自訂 R 套件 `customPackage` 加入資料庫：

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM (CONTENT = 'C:\temp\customPackage_v1.1.zip')
WITH (LANGUAGE = 'R');
GO
```
::: moniker-end

刪除 `customPackage` 程式庫。

```sql
DROP EXTERNAL LIBRARY customPackage;
```

## <a name="see-also"></a>另請參閱

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
