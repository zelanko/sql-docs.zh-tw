---
title: 從類別檔案建立 Java jar 檔案
description: 了解如何從類別檔案建立 Java jar 檔案
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a105dde9046167257a86705f678466872785b4be
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735090"
---
# <a name="create-a-java-jar-file-from-class-files"></a>從類別檔案建立 Java jar 檔案
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

了解當使用 [SQL Server 語言延伸模組](../language-extensions-overview.md)來執行 Java 程式碼時，如何將類別檔案封裝成 jar 檔案。 建議您將檔案封裝。

## <a name="create-a-jar-file"></a>建立 jar 檔案

若要從類別檔案建立 jar，請瀏覽至包含您類別檔案的資料夾，然後執行此命令：

```cmd
jar -cf <MyJar.jar> *.class
```

請確認 `jar.exe` 的路徑是系統路徑變數的一部分。 或者，指定 jar 的完整路徑，您可以在 JDK 資料夾的 `/bin` 底下找到此路徑。 例如：

```cmd
C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class
```

## <a name="next-steps"></a>後續步驟

+ [如何在 SQL Server 語言延伸模組中呼叫 Java 執行階段](../how-to/call-java-from-sql.md)