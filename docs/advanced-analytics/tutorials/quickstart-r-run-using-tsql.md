---
title: "\"Hello World\"基本 R 程式碼執行 T-SQL-SQL Server Machine Learning 中的快速入門"
description: SQL Server 中的 R 指令碼的快速入門。 了解呼叫 R 指令碼在 hello world 練習使用 sp_execute_external_script 的系統預存程序的基本概念。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1ec9580a533e51b7e99ea0ac34c1d322a27da452
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042273"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>快速入門：SQL Server 中的"Hello world"R 指令碼 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入門中，您將了解重要的概念，透過執行"Hello World"R 指令碼 inT SQL，簡介**sp_execute_external_script**系統預存程序。 

## <a name="prerequisites"></a>先決條件

先前的快速入門中，[確認 R 存在於 SQL Server](quickstart-r-verify.md)，提供資訊並連結設定本快速入門所需的 R 環境。

## <a name="basic-r-interaction"></a>基本的 R 互動

有兩種方式，您可以在 SQL Database 中執行 R 程式碼：

+ 做為引數的系統預存程序中，新增 R 指令碼[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。
+ 從[遠端 R 用戶端](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client)、 連接到您的 SQL database，並執行作為計算內容中使用 SQL Database 的程式碼。

下列練習著重於第一次的互動模型： 如何將 R 程式碼傳遞至預存程序。

1. 執行簡單的指令碼，以查看 R 指令碼如何執行您的 SQL database 中。

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))'
    '
    ```

2. 假設您有正確的正確結果所設定的所有項目會計算，以及 R`print`函式會傳回結果**訊息**視窗。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    取得時發生**stdout**訊息非常有用，測試您的程式碼時，通常您需要以表格式格式傳回結果，以便您可以在應用程式中使用它，或寫入資料表。 請參閱[快速入門：處理輸入及輸出在 SQL Server 中使用 R](rtsql-working-with-inputs-and-outputs.md)如需詳細資訊。

請記住，所有東西放在`@script`引數必須是有效的 R 程式碼。

## <a name="run-a-hello-world-script"></a>執行 Hello World 指令碼

下列練習會執行另一個簡單的 R 指令碼。

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

這個預存程序的輸入包括：

+ *@language* 參數會定義要呼叫，在此情況下，r 語言擴充功能
+ *@script* 參數會定義傳遞至 R 執行階段的命令。 您的整個 R 指令碼必須以 Unicode 文字的格式包含在此引數中。 您也可以將文字新增至 **nvarchar** 類型的變數，並呼叫該變數。
+ *@input_data_1* 會傳回查詢所傳遞至 R 執行階段，將資料傳回給 SQL Server 做為資料框架的資料。
+ 結果集子句會定義傳回的資料表的結構描述 SQL Server，將"Hello World"新增為資料行名稱，如**int**資料類型。

**結果**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>後續步驟

現在您已經執行數個簡單的 R 指令碼，看看建構輸入和輸出。

> [!div class="nextstepaction"]
> [快速入門：處理輸入和輸出](quickstart-r-inputs-and-outputs.md)
