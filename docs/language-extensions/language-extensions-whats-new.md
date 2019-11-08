---
title: 語言延伸模組的新功能
titleSuffix: SQL Server Language Extensions
description: 了解 SQL Server 2019 語言延伸模組的新功能。
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 13a6a0181297fcb05274ba4be726c4e10a445064
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73589012"
---
# <a name="what-new-in-sql-server-language-extensions"></a>SQL Server 語言延伸模組的新功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

當我們繼續擴充、延伸並加深外部語言與資料平台之間的整合時，會將[語言延伸模組](language-extensions-overview.md)功能新增至每個版本中的 SQL Server。 

## <a name="new-in-sql-server-2019"></a>SQL Server 2019 的新功能 

此版本會在 SQL Server 中加入語言延伸模組的支援。 如需此版本中所有功能的詳細資訊，請參閱 [SQL Server 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)與 [SQL Server 2019 的版本資訊](../sql-server/sql-server-ver15-release-notes.md)。

- Windows 與 Linux 上的預設 Java Runtime 是 Open Zulu JRE，隨附於 [Windows 上的 SQL Server 語言延伸模組安裝](install/install-sql-server-language-extensions-on-windows.md)與 [Linux 上的 SQL Server 語言延伸模組安裝](../linux/sql-server-linux-setup-language-extensions.md)。
- 支援的 [Java 資料類型](how-to/java-to-sql-data-types.md)。
- 在 SQL Server 中用於註冊外部語言 (例如 Java) 的 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)。
- [適用於 Java 的 Microsoft 擴充性 SDK](how-to/extensibility-sdk-java-sql-server.md)。
- 在 Windows 與 Linux 上，您可以使用 [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) 陳述式，在外部程式庫中存取 Java 程式碼。 深入了解：[如何從 SQL Server 呼叫 Java](how-to/call-java-from-sql.md)。
- Windows 與 Linux 上的 [Java 語言延伸模組](language-extensions-overview.md)。 您可以透過指派權限並設定路徑，將已編譯的 Java 程式碼提供給 SQL Server。 具有 SQL Server 存取權的用戶端應用程式可以透過呼叫 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) (SQL Server 機器學習服務上用於 R 與 Python 整合的相同程序)，來使用資料並執行程式碼。

## <a name="next-steps"></a>後續步驟

+ 安裝 [Windows 的 SQL Server 語言延伸模組](install/install-sql-server-language-extensions-on-windows.md)或 [Linux 的 SQL Server 語言延伸模組](../linux/sql-server-linux-setup-language-extensions.md)
