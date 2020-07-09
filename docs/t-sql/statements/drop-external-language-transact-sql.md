---
title: DROP EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2019
ms.prod: sql
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6f4b6ee38ed70da600ef007f168cd7e95a010278
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85766368"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

刪除現有的外部語言。

## <a name="syntax"></a>語法

```text
DROP EXTERNAL LANGUAGE <language_name>
```

### <a name="arguments"></a>引數

**language_name**

語言是資料庫範圍的物件。 語言名稱在資料庫內必須是唯一的。

## <a name="permissions"></a>權限

若要刪除語言，則需要 ALTER ANY EXTERNAL LANGUAGE 權限。 根據預設，任何資料庫擁有者或物件的擁有者，也可刪除外部語言。

> [!NOTE]
> 請注意，移除外部語言之前，您需要移除參考外部語言的外部程式庫。

### <a name="return-values"></a>傳回值

如果陳述式執行成功，會傳回參考訊息。

## <a name="remarks"></a>備註

需要先刪除指定語言的所有外部程式庫，才能刪除外部語言。

## <a name="examples"></a>範例

建立外部語言 **Java**：

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

置放外部語言：

```sql
DROP EXTERNAL LANGUAGE Java;
```

## <a name="see-also"></a>另請參閱

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
