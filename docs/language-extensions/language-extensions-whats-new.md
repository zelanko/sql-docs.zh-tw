---
title: SQL Server 語言延伸模組的新功能
titleSuffix: ''
description: 了解可擴充、延伸並加深外部語言與資料平台相互整合的 SQL Server 語言延伸模組有哪些新功能。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1583ab8c54d16d7bcf129e401c2e540fabb342b3
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155093"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>SQL Server 語言延伸模組的新功能
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

當我們繼續擴充、延伸並加深外部語言與資料平台之間的整合時，會將[語言延伸模組](language-extensions-overview.md)功能新增至每個版本中的 SQL Server。

## <a name="new-python-and-r-language-extensions-in-sql-server-2019"></a>SQL Server 2019 中新的 Python 和 R 語言延伸模組

+ 可供 [Windows 上的 Python](../machine-learning/install/custom-runtime-python.md) 使用的自訂執行階段。 若要在 Linux 上安裝，請查看[如何在 Linux 上安裝 SQL Server 適用的 Python 自訂執行階段](../machine-learning/install/custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true)。

+ 可供 [Windows 上的 R](../machine-learning/install/custom-runtime-r.md) 使用的自訂執行階段。 若要在 Linux 上安裝，請參閱[安裝適用於 Linux 上的 SQL Server 的 R 自訂執行階段](../machine-learning/install/custom-runtime-r.md?view=sql-server-linux-ver15&preserve-view=true) (英文)。


## <a name="new-java-language-extension-in-sql-server-2019"></a>SQL Server 2019 中新的 Java 語言延伸模組

如需此版本中所有功能的詳細資訊，請參閱 [SQL Server 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)與 [SQL Server 2019 的版本資訊](../sql-server/sql-server-version-15-release-notes.md)。

- Windows 與 Linux 上的預設 Java Runtime 是 Open Zulu JRE，隨附於 [Windows 上的 SQL Server 語言延伸模組安裝](install/windows-java.md)與 [Linux 上的 SQL Server 語言延伸模組安裝](../linux/sql-server-linux-setup-language-extensions-java.md)。
- 支援的 [Java 資料類型](how-to/java-to-sql-data-types.md)。
- 在 SQL Server 中用於註冊外部語言 (例如 Java) 的 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)。
- [適用於 Java 的 Microsoft 擴充性 SDK](how-to/extensibility-sdk-java-sql-server.md)。
- 在 Windows 與 Linux 上，您可以使用 [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) 陳述式，在外部程式庫中存取 Java 程式碼。 深入了解：[如何從 SQL Server 呼叫 Java](how-to/call-java-from-sql.md)。
- Windows 與 Linux 上的 [Java 語言延伸模組](language-extensions-overview.md)。 您可以透過指派權限並設定路徑，將已編譯的 Java 程式碼提供給 SQL Server。 具有 SQL Server 存取權的用戶端應用程式可以透過呼叫 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) (SQL Server 機器學習服務上用於 R 與 Python 整合的相同程序)，來使用資料並執行程式碼。

## <a name="next-steps"></a>後續步驟

+ 安裝 [Windows 的 SQL Server 語言延伸模組](install/windows-java.md)或 [Linux 的 SQL Server 語言延伸模組](../linux/sql-server-linux-setup-language-extensions-java.md)。