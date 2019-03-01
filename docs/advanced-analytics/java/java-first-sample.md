---
title: Java 範例和教學課程中的 SQL Server 2019-SQL Server Machine Learning 服務
description: 若要了解 SQL Server 資料搭配使用的 Java 語言擴充功能的步驟執行的 SQL Server 2019 上執行 Java 範例程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 86a379191033f49ab6a5d06ceda2d1ed7a747c12
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018034"
---
# <a name="sql-server-java-sample-walkthrough"></a>SQL Server 的 Java 範例逐步解說

此範例示範 Java 類別，以接收從 SQL Server 的兩個資料行 （「 識別碼 」 和 「 文字 」），並回到 SQL Server （識別碼與 ngram） 會傳回兩個資料行。 如需指定的 ID 和字串的組合，程式碼會產生排列的方式 ngrams （子字串），傳回這些排列以及原始識別碼。 Ngram 的長度是由傳送至 Java 類別的參數定義。

## <a name="prerequisites"></a>先決條件

+ SQL Server 2019 Database Engine 執行個體的擴充性架構和程式設計延伸模組的 Java[在 Windows 上](../install/sql-machine-learning-services-windows-install.md)或[on Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup)。 如需有關系統組態的詳細資訊，請參閱[Java 語言擴充功能在 SQL Server 2019](extension-java.md)。 如需有關如何撰寫程式碼需求的詳細資訊，請參閱[如何在 SQL Server 呼叫 Java](howto-call-java-from-sql.md)。

+ SQL Server Management Studio 或其他工具來執行 T-SQL。

+ Java SE Development Kit (JDK) 8 在 Windows 或 Linux。

使用命令列編譯**javac**是本教學課程。 

## <a name="1---load-sample-data"></a>1-載入範例資料

首先，建立並填入*檢閱*資料表**識別碼**並**文字**資料行。 連接到 SQL Server，然後執行下列指令碼來建立資料表：

```sql
DROP TABLE IF exists reviews;
GO
CREATE TABLE reviews(
    id int NOT NULL,
    "text" nvarchar(30) NOT NULL)

INSERT INTO reviews(id, "text") VALUES (1, 'AAA BBB CCC DDD EEE FFF')
INSERT INTO reviews(id, "text") VALUES (2, 'GGG HHH III JJJ KKK LLL')
INSERT INTO reviews(id, "text") VALUES (3, 'MMM NNN OOO PPP QQQ RRR')
GO
```

## <a name="2---class-ngramjava"></a>2-類別 Ngram.java

開始建立的主要類別。 這是三個類別中的第一個。

在此步驟中，建立類別，稱為**Ngram.java**並將下列 Java 程式碼複製到該檔案。 


```java
//We will package our classes in a package called pkg
//Packages are option in Java-SQL, but required for this sample.
package pkg;

import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Ngram {

    //Required: This is only required if you are passing data in @input_data_1
    //from SQL Server in sp_execute_external_script
    public static int[] inputDataCol1 = new int[1];
    public static String[] inputDataCol2 = new String[1];

    //Required: Input null map. Size just needs to be set to "1"
    public static boolean[][] inputNullMap = new boolean[1][1];

    //Required: Output data columns returned back to SQL Server
    public static int[] outputDataCol1;
    public static String[] outputDataCol2;

    //Required: Output null map. Is populated with true or false values 
    //to indicate nulls
    public static boolean[][] outputNullMap;

    //Optional: This is only required if parameters are passed with @params
    // from SQL Server in sp_execute_external_script
    // n is giving us the size of ngram substrings
    public static int param1;

    //Optional: The number of rows we will be returning
    public static int numberOfRows;

    //Required: Number of output columns returned
    public static short numberOfOutputCols;

    /*Java main method - Only for testing purposes outside of SQL Server
    public static void main(String... args) {
        //getNGrams();
    }*/

    //This is the method we will be calling from SQL Server
    public static void getNGrams() {

        System.out.println("inputDataCol1.length= "+ inputDataCol1.length);
        if (inputDataCol1.length == 0 ) {
            // TODO: Set empty return
            return;
        }
        //Using a stream to "loop" over the input data inputDataCol1.length. You can also use a for loop for this.
        final List<InputRow> inputDataSet = IntStream.range(0, inputDataCol1.length)
                .mapToObj(i -> new InputRow(inputDataCol1[i], inputDataCol2[i]))
                .collect(Collectors.toList());


        //Again, we are using a stream to loop over data
        final List<OutputRow> outputDataSet = inputDataSet.stream()
                // Generate ngrams of size n for each incoming string
                // Each invocation of ngrams returns a list. flatMap flattens
                // the resulting list-of-lists to a flat list.
                .flatMap(inputRow -> ngrams(param1, inputRow.text).stream().map(s -> new OutputRow(inputRow.id, s)))
                .collect(Collectors.toList());

        //Print the outputDataSet
        System.out.println(outputDataSet);

        //Set the number of rows and columns we will be returning
        numberOfOutputCols = 2;
        numberOfRows = outputDataSet.size();
        outputDataCol1 = new int[numberOfRows]; // ID column
        outputDataCol2 = new String[numberOfRows]; //The ngram column
        outputNullMap = new boolean[2][numberOfRows];// output null map

        //Since we don't have any null values, we will populate all values in the outputNullMap to false
        IntStream.range(0, numberOfRows).forEach(i -> {
            final OutputRow outputRow = outputDataSet.get(i);
            outputDataCol1[i] = outputRow.id;
            outputDataCol2[i] = outputRow.ngram;
            outputNullMap[0][i] = false;
            outputNullMap[1][i] = false;
        });
    }

    // Example: ngrams(3, "abcde") = ["abc", "bcd", "cde"].
    private static List<String> ngrams(int n, String text) {
        return IntStream.range(0, text.length() - n + 1)
                .mapToObj(i -> text.substring(i, i + n))
                .collect(Collectors.toList());
    }
}
```

## <a name="3---class-inputrowjava"></a>3 - Class InputRow.java

建立第二個類別，稱為**InputRow.java**、 組成下列程式碼，並儲存到相同的位置**Ngram.java**。

```java
package pkg;

//This object represents one input row
public class InputRow {
    public final int id;
    public final String text;

    public InputRow(final int id, final String text) {
        this.id = id;
        this.text = text;
    }
}
```

## <a name="4---class-outputrowjava"></a>4-類別 OutputRow.java

第三個也是最後一個類別即稱為**OutputRow.java**。 複製程式碼，並將儲存為 OutputRow.java 與其他相同的位置。

```java
package pkg;

//This object represents one output row
public class OutputRow {
    public final int id;
    public final String ngram;

    public OutputRow(final int id, final String ngram) {
        this.id = id;
        this.ngram = ngram;
    }

    @Override
    public String toString() { return id + ":" + ngram; }
}
```

## <a name="5---compile"></a>5-編譯

一旦就緒，您的類別執行 javac 將它們編譯成 「.class 」 檔案 (`javac Ngram.java InputRow.java OutputRow.java`)。 您應該取得 （Ngram.class InputRow.class 和 OutputRow.class），此範例的三個.class 檔案。

放在 classpath 位置稱為 「 套件 」 的子資料夾中的已編譯的程式碼。 如果您正在開發工作站上，此步驟中會是您將檔案複製到 SQL Server 電腦。

Classpath 是編譯的程式碼的位置。 比方說，在 Linux 上，如果 classpath 是 '/ home/myclasspath /'，則應該在 '/ home/myclasspath/pkg'.class 檔案。 在步驟 7 中的範例指令碼，在 sp_execute_external_script 中提供的類別路徑是 ' / home/myclasspath /' （假設 Linux）。 

在 Windows 中，我們建議使用相對較淺的資料夾結構、 一個或兩個層級，深度，以簡化權限。 比方說，您的 classpath 可能看起來像 'C:\myJavaCode' 呼叫 '\pkg' 包含已編譯的類別的子資料夾。 

如需有關 classpath 的詳細資訊，請參閱[設定 CLASSPATH](howto-call-java-from-sql.md#set-classpath)。 

### <a name="using-jar-files"></a>使用.jar 檔案

如果您計劃來封裝您的類別和.jar 檔案相依性，提供在 sp_execute_external_script CLASSPATH 參數中的.jar 檔案的完整路徑。 比方說，如果 jar 檔案稱為 'ngram.jar'，將會是 CLASSPATH ' / home/myclasspath/ngram.jar' 在 Linux 上。

## <a name="6---set-permissions"></a>6-設定權限

如果處理序身分識別可以存取您的程式碼，指令碼執行才會成功。 

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

## <a name="7---call-getngrams"></a>7 - Call *getNgrams()*

若要從 SQL Server 呼叫的程式碼，指定 Java 方法**getNgrams()** sp_execute_external_script 的"script"參數中。 這個方法屬於稱為 「 套件 」 和呼叫的類別檔案的套件**Ngram.java**。

此範例會傳遞 CLASSPATH 參數提供的 Java 檔案路徑。 它也會將參數傳遞至 Java 類別使用 「 參數 」。 請確定該 classpath 不超過 30 個字元。 若是如此，增加下列指令碼中的值。

+ 在 Linux 上，請在 SQL Server Management Studio 或其他工具，用來執行 TRANSACT-SQL 中執行下列程式碼。 

+ 在 Windows，變更@myClassPathN'C:\myJavaCode 至\'（假設它 \pkg 的上層資料夾） 中 SQL Server Management Studio 或其他工具執行查詢之前。

```sql
DECLARE @myClassPath nvarchar(50)
DECLARE @n int 
--This is where you store your classes or jars.
--Update this to your own classpath
SET @myClassPath = N'/home/myclasspath/'
--This is the size of the ngram
SET @n = 3
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.Ngram.getNGrams'
, @input_data_1 = N'SELECT id, text FROM reviews'
, @parallel = 0
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @n
with result sets ((ID int, ngram varchar(20)))
GO
```

### <a name="results"></a>結果

在執行之後呼叫，您應該會看到結果集，顯示兩個資料行：

![從 Java 範例會產生](../media/java/java-sample-results.png "範例結果")

### <a name="if-you-get-an-error"></a>如果您收到錯誤

排除 classpath 與相關的問題。 

+ Classpath 應該包含父資料夾和任何子資料夾，但不是的 「 套件 」 的子資料夾。 雖然 pkg 子資料夾必須存在，它具有不應在 classpath 中所指定值的預存程序。

+ 「 套件 」 的子資料夾應包含已編譯的程式碼，所有的三個類別。

+ Classpath 的長度不能超過宣告的值 (`DECLARE @myClassPath nvarchar(50)`)。 若是如此，路徑會被截斷成前 50 個字元，並將不會載入編譯的程式碼。 您可以執行`SELECT @myClassPath`來檢查值。 如果沒有足夠的 50 個字元的長度增加。 

+ 最後，檢查權限*每個*資料夾中，從 「 套件 」 的子資料夾，以確保執行外部處理序的安全性識別擁有讀取和執行您的程式碼的權限的根目錄。

## <a name="see-also"></a>另請參閱

+ [如何在 SQL Server 呼叫 Java](howto-call-java-from-sql.md)
+ [SQL Server 中的 Java 延伸模組](extension-java.md)
+ [Java 和 SQL Server 資料類型](java-sql-datatypes.md)
