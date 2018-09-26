---
title: 如何從 SQL 呼叫 Java |Microsoft Docs
description: 了解如何使用 Java 程式語言擴充功能在 SQL Server 2019 的 SQL Server 預存程序從呼叫 Java 類別。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08af5a18b827c783515ecd3b4ba4a802c3472f93
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715040"
---
# <a name="how-to-call-java-from-sql-server-2019"></a>如何從 SQL Server 2019 呼叫 Java

使用時[Java 語言擴充功能](extension-java.md)，則[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系統預存程序是用來呼叫的 Java 執行階段的介面。 在資料庫上的權限套用到執行 Java 程式碼。

這篇文章說明 SQL Server 上執行的 Java 類別和方法的實作詳細資料。 一旦您熟悉這些詳細資料，請檢閱[Java 範例](java-first-sample.md)在下一個步驟。

## <a name="basic-principles"></a>基本原則

* 編譯自訂的 Java 類別必須存在於.class 檔案或在您的 Java 類別路徑的.jar 檔案。 [CLASSPATH 參數](#set-classpath)提供已編譯的 Java 檔案路徑。 

* "Script"參數，預存程序中，就必須提供您要呼叫的 Java 方法。

* 如果類別所屬的封裝，就必須提供"packageName 」。

* 「 參數 」 用來將參數傳遞至 Java 類別。 需要引數的方法不支援呼叫，讓參數將引數值傳遞至方法的唯一方式。 

> [!Note]
> 本附註 restates CTP 2.0 中的 Java 特定的支援和不支援作業。
> * 預存程序中，支援的輸入的參數。 不是輸出參數。
> * 使用串流 sp_execute_external_script 的參數**@r_rowsPerRead**不支援。
> * 使用資料分割**@input_data_1_partition_by_columns**不支援。
> * 平行處理使用 **@parallel= 1**支援。

## <a name="call-spexecuteexternalscript"></a>呼叫 sp_execute_external_script

[Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)系統預存程序是用來呼叫的 Java 執行階段的介面。 下列範例示範使用參數與 Java 延伸模組，用於指定路徑、 指令碼和自訂程式碼 sp_execute_external_script。

```sql
DECLARE @myClassPath nvarchar(30)
DECLARE @param1 int

SET @myClassPath = N'/<my path>/program.jar'
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>.<methodName>'
, @input_data_1 = N'<Input Query>
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @param1
```

<a name="set-classpath"></a>

## <a name="set-classpath"></a>設定 CLASSPATH

一旦您有編譯您的 Java 類別，並置於 Java classpath 中.class 檔案或.jar 檔案，您會有兩個選項可提供給 SQL Server 的 Java 延伸模組 classpath:

**選項 1︰ 傳遞做為參數**

指定已編譯程式碼路徑的其中一個方法是將 CLASSPATH 設定為 sp_execute_external_script 程序的輸入參數。 [Java 範例](java-first-sample.md#call-method)示範這項技巧。 如果您選擇這種方法，並有多個路徑時，請務必使用適用於基礎作業系統的路徑分隔符號：

* 在 Linux 上，使用分號來分隔 CLASSPATH 中的路徑":"。
* 在 Windows 中，分隔 CLASSPATH 中的路徑以分號";"

**選項 2： 註冊系統變數**

就像您建立 JDK 的可執行檔的系統變數，您可以建立程式碼路徑的系統變數。 若要這樣做，請建立名為"CLASSPATH 」 系統環境變數

## <a name="class-requirements"></a>類別需求

為了讓 SQL Server 進行通訊的 Java 執行階段，您需要在類別中實作特定的靜態變數。 SQL Server 接著可使用的 Java 語言擴充功能的 Java 類別和交換資料中執行方法。

> [!Note]
> 預期的實作詳細資料，若要變更在即將推出的 Ctp，因為我們會致力於改善適用於開發人員體驗。

## <a name="method-requirements"></a>方法需求
若要將引數傳遞，使用**@param** sp_execute_external_script 的參數。 方法本身不能有任何引數。 傳回的型別必須是 void。  

```java
public static void test()  {}
```

## <a name="data-inputs"></a>資料輸入 

本節說明如何從 SQL Server 查詢使用時，將資料推送到 Java **InputDataSet** sp_execute_external_script 中。

為您的 SQL 查詢的推播到 Java 每個輸入資料行，您需要將陣列宣告。

### <a name="inputdatacol"></a>inputDataCol

在目前版本中的 Java 延伸模組**inputDataColN**變數是必要項，其中*N*的資料行編號。 

```java
public static <type>[] inputDataColN = new <type>[1]
```

需要先初始化這些陣列 （陣列的大小必須是大於 0，而且沒有以反映資料行的實際長度）。

範例：`public static int[] inputDataCol1 = new int[1];`

這些陣列變數會填入來自 SQL server 查詢執行的 Java 程式之前所呼叫的輸入資料。

### <a name="inputnullmap"></a>inputNullMap

延伸模組會使用 null 的對應，了解哪些值是 null。 此變數會填入 null 值的相關資訊的 SQL Server 的使用者函式執行之前。

使用者只需要將此變數 （和陣列的大小必須大於 0）。

```java
public static boolean[][] inputNullMap = new boolean[1][1];
```

## <a name="data-outputs"></a>資料輸出 

本章節描述**OutputDataSet**，Java，其中您可以將傳送至，並將保存在 SQL Server 中從傳回的輸出資料集。

> [!Note]
> 輸出中的參數[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)此版本中不支援。

### <a name="outputdatacoln"></a>outputDataColN

類似於**inputDataSet**，為您的 Java 程式會傳送回到 SQL Server 每個輸出資料行，您必須宣告陣列變數。 所有**outputDataCol**陣列應該具有相同的長度。 您必須確定這初始化類別的執行完成的時間。

```java
public static <type>[] outputDataColN = new <type>[]
```

### <a name="numberofoutputcols"></a>numberofOutputCols

此變數設為您預期使用者函式執行完成時的輸出資料行數目。

```java
public static short numberofOutputCols = <expected number of output columns>;
```

### <a name="outputnullmap"></a>outputNullMap

延伸模組會使用 null 的對應，以指出哪些值是 null。 我們需要這因為基本類型不支援 null。 目前，我們也需要 null 的對應為字串類型，即使字串可以是 null。 Null 值會以"true"。

此 NullMap 必須填入預期的資料行，您將 SQL Server 傳回的資料列數目。

```java
public static boolean[][] outputNullMap
```

## <a name="next-steps"></a>後續步驟

+ [SQL Server 中的 Java 範例](java-first-sample.md)
+ [Java 和 SQL Server 資料類型](java-sql-datatypes.md)
+ [SQL Server 中的 Java 語言擴充功能](extension-java.md)
