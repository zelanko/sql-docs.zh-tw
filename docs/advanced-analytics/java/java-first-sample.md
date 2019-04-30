---
title: Java 範例和教學課程中的 SQL Server 2019-SQL Server Machine Learning 服務
description: 若要了解 SQL Server 資料搭配使用的 Java 語言擴充功能的步驟執行的 SQL Server 2019 上執行 Java 範例程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 000318716b07f58e94bd5c482d9c349e5d4e5481
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473757"
---
# <a name="sql-server-regex-java-sample"></a>SQL Server 的 Regex Java 範例

此範例示範 Java 類別，以接收從 SQL Server 的兩個資料行 （「 識別碼 」 和 「 文字 」），並也會做為輸入參數的規則運算式。 類別會傳回兩個資料行 （「 識別碼 」 和 「 文字 」） 的 SQL Server。

針對傳送至 Java 類別的文字資料行中指定的文字，程式碼會檢查是否指定的規則運算式的履行，並傳回該文字，以及原始識別碼。 

此特定範例會使用規則運算式，以檢查如果文字包含 [Java] 或 [java] 的文字。

## <a name="microsoft-extensibility-sdk-for-java-for-microsoft-sql-server"></a>Microsoft 擴充性適用於 Microsoft SQL server 的 Java SDK

 在 CTP 2.5 中，我們會變更您實作使用的 Java 語言擴充功能與 SQL Server 通訊的 Java 程式碼的方式。 與 Java 的 SQL Server 互動時，這會提供更好的開發人員體驗。

您應該考慮的 SDK，為協助程式介面，可讓您更輕鬆地實作 SQL Server 上執行的 Java 程式碼。

> [!NOTE]
> SDK 的簡介是舊版 ctp 很大的變更。 任何先前的範例，您有工作需要更新，才能使用 SDK。

如需詳細資訊，請參閱 < [SDK 文件](java-sdk.md)。

## <a name="prerequisites"></a>先決條件

+ SQL Server 2019 Database Engine 執行個體的擴充性架構和程式設計延伸模組的 Java[在 Windows 上](../install/sql-machine-learning-services-windows-install.md)或[on Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup)。 如需有關系統組態的詳細資訊，請參閱[Java 語言擴充功能在 SQL Server 2019](extension-java.md)。 如需有關如何撰寫程式碼需求的詳細資訊，請參閱[如何在 SQL Server 呼叫 Java](howto-call-java-from-sql.md)。

+ SQL Server Management Studio 或 Azure Data Studio，來執行 T-SQL。

+ Java SE Development Kit (JDK) 8 或 JRE 8 上的 Windows 或 Linux。

+ [Microsoft SQL server 的 Microsoft Java 擴充性 SDK](http://aka.ms/mssql-java-lang-extension) mssql java-lang extension.jar。

使用命令列編譯**javac**是本教學課程。

## <a name="1---create-sample-data-in-a-sql-server-table"></a>1-在 SQL Server 資料表中建立範例資料

首先，建立並填入*testdata*資料表**識別碼**並**文字**資料行。 連接到 SQL Server，然後執行下列指令碼來建立資料表：

```sql
CREATE DATABASE javatest
GO
USE javatest
GO

-- Create table for test data
DROP TABLE IF exists testdata;
GO

CREATE TABLE testdata(
id int NOT NULL,
"text" nvarchar(100) NOT NULL)
GO

TRUNCATE TABLE testdata
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
Select * FROM testdata
```

## <a name="2---class-regexsamplejava"></a>2-類別 RegexSample.java

開始建立的主要類別。

在此步驟中，建立類別，稱為**RegexSample.java**並將下列 Java 程式碼複製到該檔案。

這個主要的類別會匯入的 SDK，也就是說，在步驟 1 中下載的 jar 檔案必須可從這個類別。

> [!NOTE]
> 請注意，此類別會匯入 Java 延伸模組 SDK 套件。
請參閱的文章[適用於 Java 的 Microsoft SQL Server 的 Microsoft 擴充性 SDK](java-sdk.md)如需詳細資訊。

```java
package pkg;

import com.microsoft.sqlserver.javalangextension.PrimitiveDataset;
import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionExecutor;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.ListIterator;
import java.util.regex.*;

public class RegexSample extends AbstractSqlServerExtensionExecutor {
    private Pattern expr;

    public RegexSample() {
        // Setup the expected extension version, and class to use for input and output dataset
        executorExtensionVersion = SQLSERVER_JAVA_LANG_EXTENSION_V1;
        executorInputDatasetClassName = PrimitiveDataset.class.getName();
        executorOutputDatasetClassName = PrimitiveDataset.class.getName();
    }
    
    public PrimitiveDataset execute(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Validate the input parameters and input column schema
        validateInput(input, params);

        int[] inIds = input.getIntColumn(0);
        String[] inValues = input.getStringColumn(1);
        int rowCount = inValues.length;

        String regexExpr = (String)params.get("regexExpr");
        expr = Pattern.compile(regexExpr);

        System.out.println("regex expression: " + regexExpr);

        // Lists to store the output data
        LinkedList<Integer> outIds = new LinkedList<Integer>();
        LinkedList<String> outValues = new LinkedList<String>();

        // Evaluate each row
        for(int i = 0; i < rowCount; i++) {
            if (check(inValues[i])) {
                outIds.add(inIds[i]);
                outValues.add(inValues[i]);
            }
        }

        int outputRowCount = outValues.size();

        int[] idOutputCol = new int[outputRowCount];
        String[] valueOutputCol = new String[outputRowCount];

        // Convert the list of output columns to arrays
        outValues.toArray(valueOutputCol);

        ListIterator<Integer> it = outIds.listIterator(0);
        int rowId = 0;

        System.out.println("Output data:");
        while (it.hasNext()) {
            idOutputCol[rowId] = it.next().intValue();

            System.out.println("ID: " + idOutputCol[rowId] + " Value: " + valueOutputCol[rowId]);
            rowId++;
        }

        // Construct the output dataset
        PrimitiveDataset output = new PrimitiveDataset();

        output.addColumnMetadata(0, "ID", java.sql.Types.INTEGER, 0, 0);
        output.addColumnMetadata(1, "Text", java.sql.Types.NVARCHAR, 0, 0);

        output.addIntColumn(0, idOutputCol, null);
        output.addStringColumn(1, valueOutputCol);

        return output;
    }

    private void validateInput(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Check for the regex expression input parameter
        if (params.get("regexExpr") == null) {
            throw new IllegalArgumentException("Input parameter 'regexExpr' is not found");
        }

        // The expected input schema should be at least 2 columns, (INTEGER, STRING)
        if (input.getColumnCount() < 2) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }

        // Check that the input column types are expected
        if (input.getColumnType(0) != java.sql.Types.INTEGER &&
                (input.getColumnType(1) != java.sql.Types.VARCHAR && input.getColumnType(1) == java.sql.Types.NVARCHAR )) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }
    }

    private boolean check(String text) {
        Matcher m = expr.matcher(text);

        return m.find();
    }
}
```

## <a name="3-compile-and-create-jar-file"></a>3 編譯，並建立.jar 檔案

我們建議您封裝您的類別和.jar 檔案相依性。 當您建置/編譯專案時，大部分的 Java Ide，例如支援 Eclipse 或 IntelliJ 產生 jar 檔案。 在此範例中，我們必須有具名的 jar 檔案**regex.jar**。

如果您要以手動方式建立.jar 檔案，您可以遵循的步驟，請參閱[如何建立的 jar 檔案](extension-java.md#create-jar)。

> [!NOTE]
> 此範例會使用封裝，這表示套件 「 套件 」 類別的頂端提供可確保已編譯的程式碼會儲存在名為 「 套件 」 的子資料夾。 這會自動處理如果您使用 IDE，但如果您以手動方式編譯使用的類別**javac**，您必須以手動方式將已編譯的程式碼置於 pkg 子資料夾。

## <a name="4---create-external-libraries"></a>4-建立外部程式庫

藉由建立外部程式庫，SQL Server 會自動具有存取 jar 檔案且您不需要任何特殊權限設 classpath。

在此範例中，您必須建立兩個外部程式庫。 其中一個 sdk，另一個用於 Regex Java 範例。

1.  下載[適用於 Java 的 Microsoft SQL Server 的 Microsoft 擴充性 SDK](http://aka.ms/mssql-java-lang-extension) mssql java-lang extension.jar。

1. 建立 sdk 的外部程式庫

```sql
-- Create external library for the SDK
CREATE EXTERNAL LIBRARY sdk
FROM (CONTENT = '<path>/mssql-java-lang-extension.jar')
WITH (LANGUAGE = 'Java');
GO
```

3. 建立外部程式庫的 regex 範例

```sql
-- Create external library for the regex sample
CREATE EXTERNAL LIBRARY regex
FROM (CONTENT = '<path>/regex.jar')
WITH (LANGUAGE = 'Java');
GO
```

## <a name="5---set-permissions-skip-if-you-performed-step-4"></a>5-設定權限 （如果您執行步驟 4 略過）

如果您使用外部程式庫，不需要執行此步驟。 工作的建議的方式是建立外部程式庫，從您的 jar。

如果您不想使用外部程式庫，您必須設定必要的權限。 如果處理序身分識別可以存取您的程式碼，指令碼執行才會成功。 您可以找到有關設定權限的詳細資訊[此處](extension-java.md)。

### <a name="on-linux"></a>在 Linux 上

授與讀取/執行權限至 classpath **mssql_satellite**使用者。

### <a name="on-windows"></a>在 Windows 上

授與 「 讀取與執行 」 權限**SQLRUserGroup**並**所有應用程式封裝**包含已編譯的 Java 程式碼的資料夾上的 SID。 

整個樹狀結構必須有權限，從根父系的最後一個子資料夾。 
 
1. 以滑鼠右鍵按一下 資料夾 (例如，' C:\myJavaCode') 中，選擇**屬性** > **安全性**。
2. 按一下 **[編輯]**。
3. 按一下 **[加入]**。
4. 在 **選取使用者、 電腦、 服務帳戶或群組**:
   + 按一下 **物件類型**，並確定*內建的安全性原則*並*群組*已選取。
   + 按一下 **位置**選取本機電腦的名稱，在清單頂端。
5. 請輸入**SQLRUserGroup**，檢查此名稱，然後按一下 [確定] 以加入群組。
6. 請輸入**ALL APPLICATION PACKAGES**，請檢查名稱，然後按一下 [確定] 以新增。 如果名稱未解決，請重新瀏覽位置步驟。 SID 是您的電腦本機。

請確定這兩個安全性身分識別具有 '讀取和執行' 的權限的資料夾和 「 套件 」 的子資料夾。

<a name="call-method"></a>

## <a name="2---call-the-java-class"></a>2-呼叫之 Java 類別

若要呼叫的 Java 程式碼，從 SQL Server，我們將建立呼叫 sp_execute_external_script 的預存程序。 在 [指令碼] 參數中，我們會定義哪一個 [套件]。[class] 我們想要呼叫。 在此範例中，此類別所屬套件，稱為**pkg**和名為類別檔案**RegexSample.java**。

> [!NOTE]
>我們不會定義要呼叫的方法。 根據預設，**執行**會呼叫方法。 這表示您需要遵循 SDK 介面，並在您的 Java 類別中實作的 execute 方法，如果您想要能夠呼叫類別從 SQL Server。

```sql
/*
This stored procedure takes an input query (input dataset) and a regular expression and returns the rows that fulfilled the given regular expression. This sample uses a regular expression that checks if a text contains the word "Java" or "java" ([Jj]ava) 
*/

CREATE OR ALTER PROCEDURE [dbo].[java_regex] @expr nvarchar(200), @query nvarchar(400)
AS
BEGIN
--Call the Java program by giving the package.className in @script
--The method invoked in the Java code is always the "execute" method
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.RegexSample'
, @input_data_1 = @query
, @params = N'@regexExpr nvarchar(200)'
, @regexExpr = @expr
with result sets ((ID int, text nvarchar(100)));
END
GO

--Now execute the above stored procedure and provide the regular expression and an input query
EXECUTE [dbo].[java_regex] N'[Jj]ava', N'SELECT id, text FROM testdata'
GO
```

### <a name="results"></a>結果

在執行之後呼叫，您應該取得結果，具有兩個資料列集。

![從 Java 範例會產生](../media/java/java-sample-results.png "範例結果")

### <a name="if-you-get-an-error"></a>如果您收到錯誤

+ 當您編譯您的類別時，「 套件 」 子資料夾應包含已編譯的程式碼，所有的三個類別。

+ 最後，如果您不使用外部程式庫，請檢查權限*每個*資料夾中，從 「 套件 」 的子資料夾，以確保執行外部處理序的安全性身分識別具有讀取和執行您的程式碼的權限的根目錄。

## <a name="next-steps"></a>後續步驟

+ [Microsoft 擴充性適用於 Microsoft SQL server 的 Java SDK](java-sdk.md)
+ [如何在 SQL Server 呼叫 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 延伸模組](extension-java.md)
+ [Java 和 SQL Server 資料類型](java-sql-datatypes.md)
