---
title: 呼叫 Java 執行階段
titleSuffix: SQL Server Language Extensions
description: 了解如何使用「SQL Server 語言延伸模組」，從 SQL Server 預存程序呼叫 Java 類別。
author: dphansen
ms.author: davidph
ms.date: 06/25/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 901410fb36080d39436a3a908a0ffd9260c5b513
ms.sourcegitcommit: 346a37242f889d76cd783f55aeed98023c693610
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91765805"
---
# <a name="how-to-call-the-java-runtime-in-sql-server-language-extensions"></a>如何在 SQL Server 語言延伸模組中呼叫 Java 執行階段
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

[SQL Server 語言延伸模組](../language-extensions-overview.md)會使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 系統預存程序，作為呼叫 Java Runtime 的介面。 

此操作說明文章會針對在 SQL Server 上執行的 Java 類別與方法，說明其實作詳細資料。

## <a name="where-to-place-java-classes"></a>Java 類別的放置位置

有兩種方法可在 SQL Server 中呼叫 Java 類別：

1. 將 **.class** 或 **.jar** 檔案放在您的 [Java Classpath](#classpath) 中。 

2. 使用[外部程式庫](#external-library) DDL，將 **.jar** 檔案中的已編譯類別與其他相依性上傳至資料庫。 

> [!NOTE]
> 一般建議使用 **.jar** 檔案，而不是個別的 **.class** 檔案。 這在 Java 中是常見的作法，可讓整體體驗變得更容易。 另請參閱[如何從類別檔案建立 jar 檔案](create-a-java-jar-file-from-class-files.md)。

<a name="classpath"></a>

## <a name="use-classpath"></a>使用 Classpath

### <a name="basic-principles"></a>基本原則

以下是在 SQL Server 上執行 Java 時的一些基本原則。

* 已編譯的自訂 Java 類別必須存在於 Java 類別路徑的 **.class** 檔案或 **.jar** 檔案中。 [CLASSPATH 參數](#set-classpath)提供已編譯之 Java 檔案的路徑。 

* 您要呼叫的 Java 方法必須在預存程序的 **script** 參數中提供。

* 如果類別屬於套件，則必須提供 **packageName**。

* **params** 是用來將參數傳遞至 Java 類別。 不支援呼叫需要引數的方法。 因此，參數是將引數值傳遞給方法的唯一方式。 

> [!NOTE]
> 此附註會重述 SQL Server 2019 候選版 1 中支援與不支援的 Java 專屬作業。
> * 在預存程序上，支援輸入參數。 輸出參數則不受支援。

### <a name="call-java-class"></a>呼叫 Java 類別

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 系統預存程序是用來呼叫 Java Runtime 的介面。 下列範例顯示使用 Java 延伸模組的 `sp_execute_external_script`，以及用來指定路徑、指令碼與自訂程式碼的參數。

> [!NOTE]
> 請注意，您不需要定義要呼叫的方法。 預設會呼叫名為 **execute** 的方法。 這表示您必須依照 [SQL Server 中適用於 Java 的擴充性 SDK](extensibility-sdk-java-sql-server.md)，並在您的 Java 類別中實作 execute 方法。

```sql
DECLARE @param1 int
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>'
, @input_data_1 = N'<Input Query>'
, @param1 = @param1
```

<a name="set-classpath"></a>

### <a name="set-classpath"></a>設定 CLASSPATH

在您編譯 Java 類別或類別，並在您的 Java Classpath 中建立 jar 檔案之後，您有兩個選項可用來提供 SQL Server Java 延伸模組的 Classpath：

1. 使用外部程式庫

    最簡單的選項是透過建立外部程式庫並將該程式庫指向 jar，讓 SQL Server 自動尋找您的類別。 [使用適用於 Java 的外部程式庫](#external-library)

2. 註冊系統環境變數

    您可以建立系統環境變數，並提供包含類別之 jar 檔案的路徑。 建立名為 **CLASSPATH** 的系統環境變數。

<a name="external-library"></a>

## <a name="use-external-library"></a>使用外部程式庫

在 SQL Server 2019 候選版 1 中，您可以在 Windows 與 Linux 上使用適用於 Java 語言的外部程式庫。 您可以將類別編譯成 .jar 檔案，並使用 [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md) DDL，將該 .jar 檔案與其他相依性上傳至資料庫。

如何使用外部程式庫上傳 .jar 檔案的範例：

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

透過建立外部程式庫，SQL Server 將會自動擁有 Java 類別的存取權，而且您不需要為 Classpath 設定任何特殊權限。

從當作外部程式庫上傳的套件呼叫類別中方法的範例：

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

如需詳細資訊，請參閱 [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)。

## <a name="loopback-connection-to-sql-server"></a>SQL Server 的回送連線

使用回送連線透過 JDBC 連線回 SQL Server，以從透過 `sp_execute_external_script` 執行的 Java 讀取和寫入資料。 當您使用 `sp_execute_external_script` 的 **InputDataSet** 與 **OutputDataSet** 引數時，無法這樣做。
若要在 Windows 內進行回送連線，請使用下列範例：

```
jdbc:sqlserver://localhost:1433;databaseName=Adventureworks;integratedSecurity=true;
``` 

若要在 Linux 內進行回送連線，JDBC 驅動程式要求在下列憑證中定義三個連線屬性：

[Client-Certificate-Authenication](https://github.com/microsoft/mssql-jdbc/wiki/Client-Certificate-Authentication-for-Loopback-Scenarios)


## <a name="next-steps"></a>後續步驟

+ [教學課程：在 Java 中使用規則運算式搜尋字串](../tutorials/search-for-string-using-regular-expressions-in-java.md)