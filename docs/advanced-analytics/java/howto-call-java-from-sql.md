---
title: 如何從 SQL-SQL Server Machine Learning 服務呼叫 Java
description: 了解如何使用 Java 程式語言擴充功能在 SQL Server 2019 的 SQL Server 預存程序從呼叫 Java 類別。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a75878ccc4f14d03f84102dd48bfd43a6e04daea
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473562"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>如何從 SQL Server 2019 預覽呼叫 Java

使用時[Java 語言擴充功能](extension-java.md)，則[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系統預存程序是用來呼叫的 Java 執行階段的介面。 在資料庫上的權限套用到執行 Java 程式碼。

這篇文章說明 SQL Server 上執行的 Java 類別和方法的實作詳細資料。 一旦您熟悉這些詳細資料，請檢閱[Java 範例](java-first-sample.md)在下一個步驟。

有兩種方法來呼叫 SQL Server 中的 Java 類別：

1. .Class 或.jar 檔案中的放置您[Java classpath](#classpath)。 這是適用於 Windows 和 Linux。

2. 上傳的.jar 檔案和資料庫使用的其他相依性中的已編譯的類別[外部程式庫](#external-library)DDL。 此選項可供 Windows 和 Linux，從 CTP 2.4。

> [!NOTE]
> 一般的建議，使用.jar 檔案並不是個別.class 檔案。 這是常見的做法，在 Java 中，而且會讓整體的體驗更輕鬆。 另請參閱：[如何從類別檔案中建立的 jar 檔案](extension-java.md#create-jar)。

<a name="classpath"></a>

## <a name="classpath"></a>Classpath

### <a name="basic-principles"></a>基本原則

* 編譯自訂的 Java 類別必須存在於.class 檔案或在您的 Java 類別路徑的.jar 檔案。 [CLASSPATH 參數](#set-classpath)提供已編譯的 Java 檔案路徑。 

* "Script"參數，預存程序中，就必須提供您要呼叫的 Java 方法。

* 如果類別所屬的封裝，就必須提供"packageName 」。

* 「 參數 」 用來將參數傳遞至 Java 類別。 需要引數的方法不支援呼叫，讓參數將引數值傳遞至方法的唯一方式。 

> [!Note]
> 本附註 restates CTP 中的 Java 特定的支援和不支援作業 2.x。
> * 預存程序中，支援的輸入的參數。 不是輸出參數。
> * 使用串流 sp_execute_external_script 參數@r_rowsPerRead不支援。
> * 資料分割使用@input_data_1_partition_by_columns不支援。
> * 平行處理使用@parallel= 1 並受到支援。

### <a name="call-java-class"></a>呼叫 Java 類別

適用於 Windows 和 Linux [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系統預存程序是用來呼叫的 Java 執行階段的介面。 下列範例示範使用參數與 Java 延伸模組，用於指定路徑、 指令碼和自訂程式碼 sp_execute_external_script。

> [!NOTE]
> 請注意，您不需要定義要呼叫的方法。 根據預設，呼叫的方法**執行**呼叫。 這表示您需要遵循 SDK，並在您的 Java 類別中實作的執行方法。

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

一次您編譯您的 Java 類別，並在您的 Java 類別路徑中建立的 jar 檔案，您有兩個選項提供給 SQL Server 的 Java 延伸模組 classpath:

**選項 1:使用外部程式庫**最簡單的選項是對 SQL Server 會自動建立外部程式庫，並指向 jar 程式庫中尋找您的類別。 [使用外部 libraries for Java](howto-call-java-from-sql.md#external-library)

**選項 2:註冊系統環境變數**

就像您會建立 Java 執行階段系統環境變數，您可以建立系統環境變數，並提供您包含類別的 jar 檔案的路徑。 若要這樣做，您需要建立名為"CLASSPATH 」 系統環境變數。

<a name="external-library"></a>

## <a name="external-library"></a>外部程式庫

在 SQL Server 2019 CTP 2.4，您可以使用外部程式庫在 Windows 和 Linux 上的 Java 語言。 您可以編譯您的類別到.jar 檔案，並將.jar 檔案和資料庫使用的其他相依性上傳[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DDL。

如何上傳的外部程式庫的.jar 檔案的範例：

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

藉由建立外部程式庫，SQL Server 會自動有 Java 類別的存取權，並不需要任何特殊權限設 classpath。

在類別中呼叫方法，從封裝的範例上傳做為外部程式庫：

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

如需詳細資訊，請參閱 < [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="next-steps"></a>後續步驟

+ [SQL Server 中的 Java 範例](java-first-sample.md)
+ [Java 和 SQL Server 資料類型](java-sql-datatypes.md)
+ [SQL Server 中的 Java 語言擴充功能](extension-java.md)
