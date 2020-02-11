---
title: 教學課程：Java 中的 Regex 字串搜尋
description: 本教學課程示範如何使用「SQL Server 語言延伸模組」，以及執行使用規則運算式 (regex) 來搜尋字串的 Java 程式碼。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9740e8c93fbac0d7727ba9922342df96d9190e10
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73658795"
---
# <a name="tutorial-search-for-a-string-using-regular-expressions-regex-in-java"></a>教學課程：在 Java 中使用規則運算式 (regex) 搜尋字串
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本教學課程示範如何使用 [SQL Server 語言延伸模組](../language-extensions-overview.md)來建立一個會從 SQL Server 接收兩個資料行 (ID 和 text) 的 Java 類別，以及一個作為輸入參數的規則運算式。 此類別會將兩個資料行傳回 SQL Server (ID 和 text)。

針對文字資料行中傳送至 Java 類別的指定文字，此程式碼會檢查指定的規則運算式是否已完成，並連同原始識別碼一起傳回該文字。

此範例程式碼會使用可檢查文字是否包含 "Java" 或 "java" 一字的規則運算式。

## <a name="prerequisites"></a>Prerequisites

+ SQL Server 2019 資料庫引擎執行個體，其中包含 [Windows](../install/install-sql-server-language-extensions-on-windows.md) 或 [Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-language-extensions) 上的擴充性架構和 Java 程式設計延伸模組。 如需詳細資訊，請參閱 [SQL Server 2019 中的語言延伸模組](../language-extensions-overview.md)。 如需有關程式碼撰寫需求的詳細資訊，請參閱[如何在 SQL Server 中呼叫 Java](../how-to/call-java-from-sql.md)。

+ 可執行 T-SQL 的 SQL Server Management Studio 或 Azure Data Studio。

+ Windows 或 Linux 上的 Java SE 開發套件 (JDK) 8或 JRE 8。

+ [適用於 Microsoft SQL Server 的 Microsoft Java 擴充性 SDK](../how-to/extensibility-sdk-java-sql-server.md) 中的 **mssql-java-lang-extension.jar** 檔案。

使用 **javac** 的命令列編譯對於本教學課程就已經足夠。

## <a name="create-sample-data"></a>建立範例資料

首先，建立新的資料庫，並將 **ID** 和 **text** 資料行填入 **testdata** 資料表中。

```sql
CREATE DATABASE javatest
GO

USE javatest
GO

CREATE TABLE testdata (
    id int NOT NULL,
    "text" nvarchar(100) NOT NULL
)
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
```

## <a name="create-the-main-class"></a>建立主類別

在此步驟中，建立名為 **RegexSample.java** 的類別檔案，並將下列 Java 程式碼複製到該檔案中。

此主類別將匯入 SDK，也就是說，在步驟 1 中下載的 jar 檔案必須可從這個類別搜尋。

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

## <a name="compile-and-create-a-jar-file"></a>編譯並建立 .jar 檔案

將您的類別和相依性封裝到 `.jar` 檔案中。 當您建置或編譯專案時，大部分的 Java IDE (例如 Eclipse 或 IntelliJ) 都支援產生 `.jar` 檔案。 將 `.jar` 檔案命名為 **regex.jar**。

如果您不是使用 Java IDE，可以手動建立一個 `.jar` 檔案。 如需詳細資訊，請參閱[如何從類別檔案建立 Java jar 檔案](../how-to/create-a-java-jar-file-from-class-files.md)。

> [!NOTE]
> 本教學課程使用封裝。 類別最上方的 `package pkg;` 行可確保已編譯的程式碼會儲存在稱為 **pkg** 的子資料夾中。 如果您使用的是 IDE，已編譯的程式碼會自動儲存在此資料夾中。 如果您使用 **javac** 手動編譯類別，則必須將已編譯的程式碼放在 **pkg** 資料夾中。

## <a name="create-external-language"></a>建立外部語言

您必須在資料庫中建立外部語言。 外部語言是資料庫範圍的物件，也就是說，需要為您想要在其中使用的每個資料庫建立 Java 之類的外部語言。

### <a name="create-external-language-on-windows"></a>在 Windows 上建立外部語言

如果您使用的是 Windows，請依照下列步驟建立適用於 Java 的外部語言。

1. 建立包含延伸模組的 .zip 檔案。

    在 Windows 上安裝 SQL Server 時，Java 延伸模組 **.zip** 檔案會安裝在這個位置：`[SQL Server install path]\MSSQL\Binn\java-lang-extension.zip`。 此 zip 檔案包含 **javaextension.dll**。

2. 從 .zip 檔案建立外部語言 Java：

    ```sql
    CREATE EXTERNAL LANGUAGE Java
    FROM
    (CONTENT = N'[SQL Server install path]\MSSQL\Binn\java-lang-extension.zip', FILE_NAME = 'javaextension.dll',
    ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"<path to JRE>"}' );
    GO
    ```

### <a name="create-external-language-on-linux"></a>在 Linux 上建立外部語言

在安裝過程中，延伸模組 **.tar.gz** 檔案會儲存在下列路徑下：`/opt/mssql-extensibility/lib/java-lang-extension.tar.gz`。

若要建立外部語言 Java，請在 Linux 上執行下列 T-SQL 陳述式：

```sql
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'/opt/mssql-extensibility/lib/java-lang-extension.tar.gz', file_name = 'javaextension.so',
ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"<path to JRE>"}' );
GO
```

### <a name="permissions-to-execute-external-language"></a>執行外部語言的權限

若要執行 Java 程式碼，使用者必須獲授與該特定語言的外部指令碼執行。

如需詳細資訊，請參閱 [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)。

## <a name="create-external-libraries"></a>建立外部程式庫

使用 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 為您的 `.jar` 檔案建立外部程式庫。 SQL Server 將可存取 `.jar` 檔案，而且您不需要將任何特殊權限設定為 **classpath**。

在此範例中，您將建立兩個外部程式庫。 一個用於 SDK，另一個用於 RegEx Java 程式碼。

1. SDK jar 檔案 **mssql-java-lang-extension.jar** 會在 Windows 和 Linux 上安裝為 SQL Server 2019 的一部分。

    + Windows 上的預設安裝路徑： **[執行個體安裝主目錄]\MSSQL\Binn\mssql-java-lang-extension.jar**

    + Linux 上的預設安裝路徑： **/opt/mssql/lib/mssql-java-lang-extension.jar**

    此程式碼也是開放原始碼，而且可以在 [SQL Server 語言延伸模組 GitHub 存放庫](https://github.com/microsoft/sql-server-language-extensions)中找到。 如需詳細資訊，請參閱[適用於 Java for Microsoft SQL Server 的 Microsoft 擴充性 SDK](../how-to/extensibility-sdk-java-sql-server.md)。

2. 建立適用於 SDK 的外部程式庫。

    ```sql
    CREATE EXTERNAL LIBRARY sdk
    FROM (CONTENT = '<OS specific path from above>/mssql-java-lang-extension.jar')
    WITH (LANGUAGE = 'Java');
    GO
    ```

3. 建立適用於 RegEx 程式碼的外部程式庫。

    ```sql
    CREATE EXTERNAL LIBRARY regex
    FROM (CONTENT = '<path>/regex.jar')
    WITH (LANGUAGE = 'Java');
    GO
    ```

## <a name="set-permissions"></a>設定權限

> [!NOTE]
> 如果您在上一個步驟中使用外部程式庫，請略過此步驟。 建議的方式是從您的 `.jar` 檔案建立外部程式庫。

如果您不想要使用外部程式庫，則必須設定所需的權限。 只有在處理序識別可存取您的程式碼時，指令碼執行才會成功。 您可以在[安裝指南](../install/install-sql-server-language-extensions-on-windows.md)中找到設定權限的詳細資訊。

### <a name="on-linux"></a>在 Linux 上

將 classpath 的讀取/執行權限授與 **mssql_satellite** 使用者。

### <a name="on-windows"></a>在 Windows 上

在包含已編譯之 Java 程式碼的資料夾中，將「讀取和執行」權限授與 **SQLRUserGroup** 和**所有應用程式封裝** SID。

整個樹狀結構都必須擁有權限 (從根父系到最後一個子資料夾)。

1. 以滑鼠右鍵按一下資料夾 (例如 `C:\myJavaCode`)，然後選擇 [內容]   > [安全性]  。
2. 按一下 **[編輯]** 。
3. 按一下 [新增]  。
4. 在 [選取使用者、電腦、服務帳戶或群組]  中：
   1. 按一下 [物件類型]  ，並確定已選取 [內建安全性原則]  和 [群組]  。
   2. 按一下 [位置]  ，選取清單頂端的本機電腦名稱。
5. 輸入 **SQLRUserGroup**、檢查名稱，然後按一下 [確定] 以新增群組。
6. 輸入 **ALL APPLICATION PACKAGES**、檢查名稱，然後按一下 [確定] 以新增。 
    如果名稱無法解析，請重新瀏覽「位置」步驟。 SID 在您電腦的本機上。

請確定這兩個安全性識別都有資料夾以及 **pkg** 子資料夾的 [讀取和執行]  權限。

<a name="call-method"></a>

## <a name="call-the-java-class"></a>呼叫 Java 類別

建立一個可呼叫 `sp_execute_external_script` 的預存程序，以便從 SQL Server 呼叫 Java 程式碼。 在 **script** 參數中，定義您要呼叫的 `package.class`。 在下列程式碼中，類別屬於稱為 **pkg** 的封裝，以及稱為 **RegexSample.java** 的類別檔案。

> [!NOTE]
> 此程式碼不會定義要呼叫的方法。 根據預設，將會呼叫 **execute** 方法。 也就是說，如果您想要能夠從 SQL Server 呼叫類別，則必須遵循 SDK 介面，並在您的 Java 類別中實作執行方法。

預存程序會採用輸入查詢 (輸入資料集) 和規則運算式，並傳回滿足指定規則運算式的資料列。 它會使用可檢查文字是否包含 **Java** 或 **java** 這個字的規則運算式 `[Jj]ava`。

```sql
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

執行呼叫之後，您應該會獲得包含其中兩個資料列的結果集。

![Java 範例的結果](../media/java/java-sample-results.png "範例結果")

### <a name="if-you-get-an-error"></a>如果您收到錯誤

+ 當您編譯類別時，**pkg** 子資料夾應該包含全部三個類別的已編譯器程式碼。

+ 如果您沒有使用外部程式庫，請檢查*每個*資料夾的權限 (從 **root** 到 **pkg** 子資料夾)，以確保執行外部處理序的安全性識別擁有讀取和執行程式碼的權限。

## <a name="next-steps"></a>後續步驟

+ [如何在 SQL Server 中呼叫 Java](../how-to/call-java-from-sql.md)
+ [SQL Server 中的 Java 延伸模組](../language-extensions-overview.md)
+ [Java 和 SQL Server 資料類型](../how-to/java-to-sql-data-types.md)
