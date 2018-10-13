---
title: SQL Server Machine Learning 服務的權限授與使用者 |Microsoft Docs
description: 如何為使用者提供 SQL Server Machine Learning 服務的權限。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ad5c3fa3bf94bb88041c9ec81773b2a26013e517
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100329"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>SQL Server Machine Learning 服務的權限授與使用者
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何您能給予使用者權限在 SQL Server Machine Learning 服務執行外部指令碼，並提供讀取、 寫入或資料定義語言 (DDL) 資料庫的權限。

SQL Server 登入或 Windows 使用者帳戶，才能執行外部指令碼，使用 SQL Server 資料，或包含執行與 SQL Server 計算內容。

登入或使用者帳戶識別*安全性主體*，可能需要多個層級的存取，根據外部指令碼需求的使用者：

+ 存取的資料庫，啟用外部指令碼的權限。
+ 若要從受保護的物件，例如資料表讀取資料的權限。
+ 能夠將新的資料寫入至資料表，例如模型或評分結果。
+ 能夠建立新的物件，例如資料表、 預存程序，使用外部指令碼，或自訂函式，該使用 R 或 Python 作業。
+ SQL Server 電腦上安裝新套件或使用套件提供給一群使用者權限。

因此，每個執行外部指令碼，為的執行內容中使用 SQL Server 的人必須對應至資料庫中的使用者。 在 SQL Server 安全性下，很容易建立角色，以管理集合的權限，並將使用者指派給這些角色，而不是個別設定 使用者權限。

在 外部工具中使用 R 或 Python 的使用者必須對應至登入或資料庫中的帳戶，如果使用者需要執行外部指令碼在資料庫或 access 資料庫物件和資料。 外部指令碼是否會從遠端資料科學用戶端傳送，或使用 T-SQL 預存程序啟動，不需要使用相同的權限。

例如，假設您建立您的本機電腦上執行外部指令碼，以及您想要在 SQL Server 上執行該程式碼。 您必須確認符合下列條件：

+ 該資料庫允許遠端連線。
+ SQL 登入或您用來進行資料庫存取權的 Windows 帳戶已新增至 SQL Server 執行個體層級。
+ SQL 登入或 Windows 使用者必須執行外部指令碼的權限。 一般而言，只有資料庫管理員可以授與此權限。
+ SQL 登入或 Window 使用者必須新增為使用者，具有適當的權限，其中外部指令碼會執行任何這些作業的每個資料庫中：
  + 正在擷取資料。
  + 寫入或更新資料。
  + 建立新的物件，例如資料表或預存程序。

登入或 Windows 使用者帳戶已佈建並具有必要的權限之後，您可以藉由在 R 中使用資料來源物件在 SQL Server 上執行外部指令碼或**revoscalepy**在 Python 中，或藉由呼叫預存的程式庫包含外部指令碼的程序。

從 SQL Server 啟動外部指令碼時，每當資料庫引擎安全性取得啟動工作，及管理對應的使用者或登入安全性實體物件之使用者的安全性內容。

因此，從遠端用戶端起始的所有外部指令碼必須登入或使用者資訊指定為連接字串的一部分。

<a name="permissions-external-script"></a> 

## <a name="permission-to-run-scripts"></a>若要執行指令碼的權限

如果您已安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而且您會在您自己的執行個體中執行 R 或 Python 指令碼，您通常會以系統管理員身分執行指令碼。 因此，您會有隱含權限不同作業和資料庫中的所有資料。

不過，大部分的使用者，不需要這類更高的權限。 例如，在組織中使用 SQL 登入通常存取資料庫的使用者沒有提高權限。 因此，對於每個使用者使用 R 或 Python，您必須授與使用者的機器學習服務會使用語言每個資料庫中執行外部指令碼的權限。 方法：

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
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