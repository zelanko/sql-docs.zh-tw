---
title: 授與指令碼的權限
description: 如何在 SQL Server 機器學習服務上授與可執行 R 和 Python 指令碼的資料庫使用者權限。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9b8d3ea5c52c5c18f09097322fdc1e1b2321494e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727304"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>授與使用者 SQL Server 機器學習服務的權限
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何對使用者授與在 SQL Server 機器學習服務中執行外部指令碼的權限，並將讀取、寫入或資料定義語言 (Data Definition Language，DDL) 權限授與資料庫。

如需詳細資訊，請在[擴充性架構的安全性概觀](../../advanced-analytics/concepts/security.md#permissions)中參閱＜權限＞區段。

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>執行指令碼的權限

如果您已自行安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而且是在自己的執行個體中執行 R 或 Python 指令碼，您通常會以系統管理員的身分執行指令碼。 因此，您有資料庫中各種作業和所有資料的隱含權限。

不過，大部分的使用者並沒有這麼高的權限。 例如，組織中使用 SQL 登入來存取資料庫的使用者通常不會有較高的權限。 因此，對於使用 R 或 Python 的每位使用者，您都必須將權限授與機器學習服務的使用者，使其可以在使用該語言的每個資料庫中執行外部指令碼。 方法：

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 權限並非限定於支援的指令碼語言。 換句話說，R 指令碼與 Python 指令碼並沒有不同的權限層級。 如果您需要針對這些語言維護個別的權限，請在不同的執行個體上安裝 R 和 Python。

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>授與資料庫權限

當使用者執行指令碼時，使用者可能需要讀取其他資料庫的資料。 使用者也可能需要建立新的資料表來儲存結果，並將資料寫入資料表。

對於執行 R 或 Python 指令碼的每個 Windows 使用者帳戶或 SQL 登入，請確定其具有特定資料庫的適當權限：用於讀取資料的 `db_datareader`、用於將物件儲存至資料庫的 `db_datawriter`，或是用於建立物件 (例如包含已定型和序列化資料的預存程序或資料表) 的 `db_ddladmin`。

例如，下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式提供 SQL 登入 *MySQLLogin* 在  資料庫中執行 T-SQL 查詢的權限。 SQL 登入必須存在於伺服器的安全性內容中，才能執行此陳述式。

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>後續步驟

如需每個角色中所包含的權限詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。