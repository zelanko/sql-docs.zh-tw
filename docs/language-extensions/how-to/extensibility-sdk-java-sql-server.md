---
title: 適用於 Java 的 Microsoft 擴充性 SDK
description: 了解如何使用「適用於 Java 的 Microsoft 擴充性 SDK」來實作適用於 SQL Server 的 Java 程式。
ms.prod: sql
ms.technology: language-extensions
ms.date: 11/05/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 011d8ba2e9c92d0df6fe2956c190f61934948f54
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870130"
---
# <a name="microsoft-extensibility-sdk-for-java-for-sql-server"></a>適用於 SQL Server 的 Microsoft Extensibility SDK for Java
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

了解如何使用「適用於 Java 的 Microsoft 擴充性 SDK」來實作適用於 SQL Server 的 Java 程式。 SDK 是 Java 語言延伸模組的介面，可用來與 SQL Server 交換資料，並從 SQL Server 執行 Java 程式碼。

SDK 在 Windows 與 Linux 上安裝為 SQL Server 2019 候選版 1 的一部分：

+ Windows 上的預設安裝路徑：**[執行個體安裝主目錄]\MSSQL\Binn\mssql-java-lang-extension.jar**
+ Linux 上的預設安裝路徑：**/opt/mssql/lib/mssql-java-lang-extension.jar**

此程式碼是開放原始碼，而且可以在 [SQL Server 語言延伸模組 GitHub 存放庫](https://github.com/microsoft/sql-server-language-extensions)中找到。

## <a name="implementation-requirements"></a>實作需求

SDK 介面會定義一組需求，必須滿足這組需求，SQL Server 才能與 Java Runtime 進行通訊。 若要使用 SDK，您必須在主要類別中遵循一些實作規則。 之後，SQL Server 可以執行 Java 類別中的特定方法，並使用 Java 語言延伸模組交換資料。

如需如何使用 SDK 的範例，請參閱[教學課程：在 Java 中使用規則運算式 (regex) 搜尋字串](../tutorials/search-for-string-using-regular-expressions-in-java.md)。

## <a name="sdk-classes"></a>SDK 類別

SDK 是由三個類別所組成。

以下兩個抽象類別會定義 Java 延伸模組用來與 SQL Server 交換資料的介面：

- **AbstractSqlServerExtensionExecutor**
- **AbstractSqlServerExtensionDataset**

第三個類別是 helper 類別，其中包含資料集物件的實作。 這是選用的類別，可讓您更輕鬆地開始使用。 您也可以改為使用自己的此類類別實作。

- **PrimitiveDataset**

您可以在下面找到 SDK 中每個類別的描述。 您可以在 [SQL Server 語言延伸模組 GitHub 存放庫](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/java/sdk)中找到 SDK 類別的原始程式碼。

### <a name="class-abstractsqlserverextensionexecutor"></a>類別：AbstractSqlServerExtensionExecutor

抽象類別 **AbstractSqlServerExtensionExecutor** 包含適用於 SQL Server 的 Java 語言延伸模組用來執行 java 程式碼的介面，。

您的主要 Java 類別必須繼承自此類別。 繼承自此類別表示類別中有您必須在自己的類別中實作的特定方法。

若要繼承自這個抽象類別，您可以在類別宣告中使用抽象類別名稱來擴充：

```java
public class <MyClass> extends AbstractSqlServerExtensionExecutor {}
```

您的主要類別至少必須實作 execute(...) 方法。

#### <a name="method-execute"></a>execute 方法

execute 方法是從 SQL Server 透過 Java 語言延伸模組呼叫的方法，用來從 SQL Server 叫用 Java 程式碼。 這是一個重要的方法，其中包含您想要從 SQL Server 執行的主要作業。

若要從 SQL Server 將方法引數傳遞至 Java，請在 `sp_execute_external_script` 中使用 `@param` 參數。 **execute** 方法會以該方式接受其引數。

```java
public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params)  {}
```

#### <a name="method-init"></a>init 方法

init 方法會在建構函式之後和 execute 方法之前執行。 需要在 execute(...) 之前執行的任何作業都可以使用這個方法來完成。

```java
public void init(String sessionId, int taskId, int numtask) {}
```

### <a name="class-abstractsqlserverextensiondataset"></a>類別：AbstractSqlServerExtensionDataset

抽象類別 **AbstractSqlServerExtensionDataset** 包含用來處理 Java 延伸模組所使用之輸入和輸出資料的介面。


### <a name="class-primitivedataset"></a>類別：PrimitiveDataset

類別 **PrimitiveDataset** 是將簡單類型儲存為基本陣列之 **AbstractSqlServerExtensionDataset** 的實作。

它在 SDK 中是以選用的協助程式類別形式提供。 如果您不使用這個類別，則必須實作您自己繼承自 **AbstractSqlServerExtensionDataset** 的類別。  

## <a name="next-steps"></a>後續步驟

+ [教學課程：在 Java 中使用規則運算式 (regex) 搜尋字串](../tutorials/search-for-string-using-regular-expressions-in-java.md)
+ [如何在 SQL Server 中呼叫 Java](call-java-from-sql.md)
