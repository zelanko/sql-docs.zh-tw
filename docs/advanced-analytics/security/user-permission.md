---
title: SQL Server Machine Learning 服務的權限授與使用者 |Microsoft Docs
description: 如何為使用者提供 SQL Server Machine Learning 服務的權限。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 07268386ad66350eed7f1382348fa4d698863600
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419063"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>SQL Server Machine Learning 服務的權限授與使用者
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何您能給予使用者權限在 SQL Server Machine Learning 服務執行外部指令碼，並提供讀取、 寫入或資料定義語言 (DDL) 資料庫的權限。

如需詳細資訊，請參閱中的 [權限] 區段[擴充性架構的安全性概觀](../../advanced-analytics/concepts/security.md#permissions)。

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>若要執行指令碼的權限

如果您已安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而且您會在您自己的執行個體中執行 R 或 Python 指令碼，您通常會以系統管理員身分執行指令碼。 因此，您會有隱含權限不同作業和資料庫中的所有資料。

不過，大部分的使用者，不需要這類更高的權限。 例如，在組織中使用 SQL 登入通常存取資料庫的使用者沒有提高權限。 因此，對於每個使用者使用 R 或 Python，您必須授與使用者的機器學習服務會使用語言每個資料庫中執行外部指令碼的權限。 方法：

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 不支援的指令碼語言特定的權限。 換句話說，沒有與 Python 指令碼的 R 指令碼的個別權限層級。 如果您需要維護這些語言的個別權限，請個別執行個體上安裝 R 和 Python。

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Grant 資料庫權限

當使用者執行指令碼時，使用者可能需要讀取其他資料庫中的資料。 使用者可能也需要建立新的資料表來儲存結果，並將資料寫入至資料表。

對於每個 Windows 使用者帳戶或 SQL 登入執行 R 或 Python 指令碼，請確定它在特定資料庫上擁有適當的權限：`db_datareader`來讀取資料，`db_datawriter`若要將物件儲存到資料庫，或`db_ddladmin`建立物件例如，預存程序或資料表包含訓練和序列化資料。

例如，下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式可提供 SQL 登入*MySQLLogin*執行的 T-SQL 查詢的權限*ML_Samples*資料庫。 SQL 登入必須存在於伺服器的安全性內容中，才能執行此陳述式。

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>後續步驟

如需包含在每個角色的權限的詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。