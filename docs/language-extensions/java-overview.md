---
title: 什麼是 Java 語言延伸模組？
titleSuffix: SQL Server Language Extensions
description: Java 語言延伸模組是 SQL Server 的功能，用來執行外部 Java 程式碼。 透過使用擴充性架構，即可在外部 Java 程式碼中使用關聯式資料。
author: dphansen
ms.author: davidph
ms.date: 11/10/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6489ce49a1236f65ef5ff2fec677327bd6a7f84e
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549982"
---
# <a name="what-is-java-language-extension"></a>什麼是 Java 語言延伸模組？
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

Java 語言延伸模組是 SQL Server 的功能，用來執行外部 Java 程式碼。 透過使用[擴充性架構](concepts/extensibility-framework.md)，即可在外部 Java 程式碼中使用關聯式資料。 Java 語言延伸模組是 [SQL Server 語言延伸模組](language-extensions-overview.md)的一部分。

預設的 Java Runtime 是 Zulu Open JRE。 您也可以使用另一個 Java JRE 或 SDK。

## <a name="what-you-can-do-with-the-java-language-extension"></a>Java 語言延伸模組的用途

Java 語言延伸模組會使用擴充性架構來執行外部 Java 程式碼。 程式碼執行與核心引擎流程隔離，但與 SQL Server 查詢執行完全整合。 您可以在資料來源執行 Java 程式碼，而不必透過網路提取資料。

外部 Java 語言是使用 [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql) 定義的。 系統預存程序 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) \(部分機器翻譯\) 是用來當作執行 Java 程式碼的介面使用。

## <a name="get-started-with-java-language-extension"></a>開始使用 Java 語言延伸模組

1. 在 [Windows](install/windows-java.md) 或 [Linux](../linux/sql-server-linux-setup-language-extensions-java.md) 上安裝 SQL Server Java 語言延伸模組。

1. 設定開發工具。

    + 使用您慣用的 IDE 開發 Java 程式碼。
    + 安裝[適用於 Java 的 Microsoft 擴充性 SDK](how-to/extensibility-sdk-java-sql-server.md)，以在 SQL Server 上執行 Java 程式碼。
    + 使用 [Azure Data Studio](../azure-data-studio/what-is.md) 來在 SQL Server 上執行外部程式碼。
    + 使用系統預存程序 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)，在 SQL Server 上執行 Java 程式碼。

1. 撰寫您的第一個 Java 程式碼。

    + [教學課程：使用 Java 的規則運算式](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>限制

輸入和輸出緩衝區中的值數目不得超過 `MAX_INT (2^31-1)`，因為這是可在 Java 中以陣列配置的元素數目上限。

## <a name="next-steps"></a>後續步驟

+ 在 [Windows](install/windows-java.md) 或 [Linux](../linux/sql-server-linux-setup-language-extensions-java.md) 上安裝 SQL Server Java 語言延伸模組
+ 安裝[適用於 Java 的 Microsoft 擴充性 SDK](how-to/extensibility-sdk-java-sql-server.md)
