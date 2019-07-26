---
title: 授與 R 和 Python 腳本執行的資料庫許可權
description: 如何在 SQL Server Machine Learning 服務上授與資料庫使用者權限以進行 R 和 Python 腳本的執行。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: be6d23c6b176e8d7b2c9bf0d7ff7a02212509a10
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469834"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>授與使用者 SQL Server Machine Learning 服務的許可權
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何授與使用者在 SQL Server Machine Learning 服務中執行外部腳本的許可權, 並將讀取、寫入或資料定義語言 (DDL) 許可權授與資料庫。

如需詳細資訊, 請參閱擴充性[架構的安全性總覽](../../advanced-analytics/concepts/security.md#permissions)中的許可權一節。

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>執行腳本的許可權

如果您自行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝, 而且您在自己的實例中執行 R 或 Python 腳本, 您通常會以系統管理員身分執行腳本。 因此, 您對各種作業和資料庫中的所有資料具有隱含許可權。

不過, 大部分的使用者並沒有這麼高的許可權。 例如, 組織中使用 SQL 登入來存取資料庫的使用者, 通常不會有較高的許可權。 因此, 對於使用 R 或 Python 的每位使用者, 您必須授與 Machine Learning 服務的使用者在使用該語言的每個資料庫中執行外部腳本的許可權。 方法：

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 許可權並非特定于支援的指令碼語言。 換句話說, R 腳本與 Python 腳本並沒有個別的許可權層級。 如果您需要維護這些語言的個別許可權, 請在不同的實例上安裝 R 和 Python。

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>授與資料庫許可權

當使用者執行腳本時, 使用者可能需要讀取其他資料庫的資料。 使用者也可能需要建立新的資料表來儲存結果, 並將資料寫入資料表。

對於執行 R 或 Python 腳本的每個 Windows 使用者帳戶或 SQL 登入, 請確定它具有特定資料庫的適當許可權: `db_datareader`讀取資料、 `db_datawriter`將物件儲存至資料庫, 或`db_ddladmin`建立物件例如預存程式或包含定型和序列化資料的資料表。

例如, 下列[!INCLUDE[tsql](../../includes/tsql-md.md)]語句提供 SQL 登入*MySQLLogin*在*ML_Samples*資料庫中執行 t-SQL 查詢的許可權。 SQL 登入必須存在於伺服器的安全性內容中，才能執行此陳述式。

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>後續步驟

如需每個角色中所包含之許可權的詳細資訊, 請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。