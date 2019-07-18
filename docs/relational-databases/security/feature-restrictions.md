---
title: 功能限制 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 99a0a768334ab5335591fae69e4f18060fba9866
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506916"
---
# <a name="feature-restrictions"></a>功能限制

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 攻擊的一個常見來源是透過 Web 應用程式，它會存取資料庫，使用各種形式的 SQL 插入式攻擊搜集資料庫的相關資訊。  在理想情況下，因為應用程式程式碼已開發，因此不允許 SQL 插入式攻擊。  不過，在摻雜舊版和外部程式碼的大型程式碼基底中，無人可以百分百確定所有的情況皆已處理，所以在現實生活中，SQL 插入式攻擊不可不防。  功能限制目的是為了防止某些形式的 SQL 插入洩漏資料庫資訊，即使是 SQL 插入成功時。

## <a name="enabling-feature-restrictions"></a>啟用功能限制

使用 `sp_add_feature_restriction` 預存程序即可啟用功能限制，如下所示：

```sql
EXEC sp_add_feature_restriction <feature>, <object_class>, <object_name>
```

您可限制下列功能：

| 功能          | Description |
|------------------|-------------|
| N'ErrorMessages' | 限制時，會遮罩錯誤訊息中的任何使用者資料。 請參閱[錯誤訊息功能限制](#error-messages-feature-restriction) |
| N'Waitfor'       | 限制時，此命令會立即傳回，毫無延遲。 請參閱 [WAITFOR 功能限制](#waitfor-feature-restriction) |

`object_class` 值可以是 `N'User'` 或 `N'Role'`，以表示 `object_name` 為資料庫中的使用者名稱或角色名稱。

下列範例會遮罩使用者 `MyUser` 的所有錯誤訊息：

```sql
EXEC sp_add_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="disabling-feature-restrictions"></a>停用功能限制

使用 `sp_drop_feature_restriction` 預存程序即可停用功能限制，如下所示：

```sql
EXEC sp_drop_feature_restriction <feature>, <object_class>, <object_name>
```

下列範例會停用使用者 `MyUser` 的錯誤訊息遮罩：

```sql
EXEC sp_drop_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="viewing-feature-restrictions"></a>檢視功能限制

`sys.sql_feature_restrictions` 檢視會顯示資料庫目前所有定義的功能限制。 如需詳細資訊，請參閱 [sys.sql_feature_restrictions](../system-catalog-views/sys-sql-feature-restrictions.md)。

## <a name="feature-restrictions"></a>功能限制

### <a name="error-messages-feature-restriction"></a>錯誤訊息功能限制

一個常見 SQL 插入式攻擊方法是插入會造成錯誤的程式碼。  攻擊者可以藉由檢查錯誤訊息，深入了解系統相關資訊，發動其他更具針對性的攻擊。  這種攻擊對不顯示查詢結果，卻顯示錯誤訊息的應用程式特別有用。

請考慮要求形式如下的 Web 應用程式：

```html
http://www.contoso.com/employee.php?id=1
```

它會執行下列資料庫查詢：

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

如果複製當作 `Id` 參數傳遞給 Web 應用程式要求的值來取代資料庫查詢中 $EmpId，則攻擊者可能會提出下列要求：

```html
http://www.contoso.com/employee.php?id=1 AND CAST(DB_NAME() AS INT)=0
```

可能會傳回下列錯誤，讓攻擊者了解資料庫的名稱：

```sql
Conversion failed when converting the nvarchar value 'HR_Data' to data type int.
```

針對資料庫的應用程式使用者啟用錯誤訊息功能限制之後，即會遮罩傳回的錯誤訊息，不洩漏資料庫的任何內部資訊：

```sql
Conversion failed when converting the ****** value '******' to data type ******.
```

同樣地，攻擊者可以提出下列要求：

```html
http://www.contoso.com/employee.php?id=1 AND CAST(Salary AS TINYINT)=0
```

可能會傳回下列錯誤，讓攻擊者了解員工薪資：

```sql
Arithmetic overflow error for data type tinyint, value = 140000.
```

使用錯誤訊息功能限制，資料庫可能傳回：

```sql
Arithmetic overflow error for data type ******, value = ******.
```

### <a name="waitfor-feature-restriction"></a>WAITFOR 功能限制

密件 SQL 插入是應用程式不向攻擊者提供插入的 SQL 結果或錯誤訊息，但攻擊者可以建構條件式查詢，使用執行時間不同的兩個條件式分支來推斷資料庫資訊。 藉由比較回應時間，攻擊者可以知道哪個分支已執行，進而了解系統的相關資訊。 這類攻擊最簡單的變體是使用 `WAITFOR` 陳述式來導入延遲。

請考慮要求形式如下的 Web 應用程式：

```html
http://www.contoso.com/employee.php?id=1
```

它會執行下列資料庫查詢：

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

如果複製當作 `Id` 參數傳遞給 Web 應用程式要求的值來取代資料庫查詢中 $EmpId，則攻擊者可以提出下列要求：

```html
http://www.contoso.com/employee.php?id=1; IF SYSTEM_USER='sa' WAITFOR DELAY '00:00:05'
```

如有 `sa` 帳戶正在使用中，則查詢會多花 5 秒。 如果資料庫停用 `WAITFOR` 功能限制，則會忽略 `WAITFOR` 陳述式，且不會使用這種攻擊來外洩資訊。
