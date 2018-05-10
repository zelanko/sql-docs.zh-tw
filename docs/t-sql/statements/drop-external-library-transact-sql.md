---
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/05/2018
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b72dd7a41e4d7cca0988ac28efd0f9cb60ca739
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

刪除現有的套件程式庫。 支援的外部執行階段 (例如 R 或 Python) 會使用套件程式庫。

## <a name="syntax"></a>語法

```sql
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

## <a name="permissions"></a>Permissions

若要刪除程式庫，需要 ALTER ANY EXTERNAL LIBRARY 權限。 根據預設，任何資料庫擁有者或物件的擁有者，也可刪除外部程式庫。

### <a name="return-values"></a>傳回值

如果陳述式執行成功，會傳回參考訊息。

## <a name="remarks"></a>Remarks

不同於 SQL Server 中的其他 `DROP` 陳述式，此陳述式支援指定選擇性授權子句。 這可讓 **db_owner** 角色中的 **dbo** 或使用者卸除資料庫中由一般使用者上傳的套件資料庫。

## <a name="examples"></a>範例

將自訂 R 套件 `customPackage` 加入資料庫：

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM (CONTENT = 'C:\temp\customPackage_v1.1.zip')
WITH (LANGUAGE = 'R');
GO
```

刪除 `customPackage` 程式庫。

```sql
DROP EXTERNAL LIBRARY customPackage;
```

## <a name="see-also"></a>另請參閱

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

