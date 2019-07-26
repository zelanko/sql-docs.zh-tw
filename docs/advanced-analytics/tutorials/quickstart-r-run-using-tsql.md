---
title: 在 T-sql 中執行「Hello World」基本 R 程式碼的快速入門
description: SQL Server 中 R 腳本的快速入門。 瞭解在 hello world 練習中使用 sp_execute_external_script 系統預存程式呼叫 R 腳本的基本概念。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ab73e0231f462504652e0e1af62fed80c706f061
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469041"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>快速入門：SQL Server 中的 "Hello world" R 腳本 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入門中, 您可以藉由執行「Hello World」 R 腳本 inT-SQL 來瞭解重要概念, 其中包含**sp_execute_external_script**系統預存程式的簡介。 

## <a name="prerequisites"></a>先決條件

先前的快速入門[中, 驗證 R 存在於 SQL Server 中](quickstart-r-verify.md), 提供設定本快速入門所需之 R 環境的相關資訊和連結。

## <a name="basic-r-interaction"></a>基本 R 互動

有兩種方式可以在 SQL Database 中執行 R 程式碼:

+ 將 R 腳本新增為系統預存程式[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)的引數。
+ 從[遠端 R 用戶端](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client), 連接到您的 SQL 資料庫, 然後使用 SQL Database 作為計算內容來執行程式碼。

下列練習著重于第一個互動模型: 如何將 R 程式碼傳遞至預存程式。

1. 執行簡單的腳本, 以查看 R 腳本如何在您的 SQL 資料庫中執行。

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

2. 假設您已正確設定正確的結果, 且 R `print`函式將結果傳回至 [**訊息**] 視窗。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    在測試您的程式碼時, 取得**stdout**訊息很有用, 但您通常需要以表格格式傳回結果, 以便在應用程式中使用它或將其寫入資料表。 請[參閱快速入門:在 SQL Server](rtsql-working-with-inputs-and-outputs.md)中使用 R 來處理輸入和輸出, 以取得詳細資訊。

請記住, 引數`@script`內的所有專案都必須是有效的 R 程式碼。

## <a name="run-a-hello-world-script"></a>執行 Hello World 腳本

下列練習會執行另一個簡單的 R 腳本。

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

此預存程式的輸入包括:

+ *@language* 參數會定義要呼叫的語言擴充功能, 在此案例中為 R。
+ *@script* 參數會定義傳遞至 R 執行時間的命令。 您的整個 R 指令碼必須以 Unicode 文字的格式包含在此引數中。 您也可以將文字新增至 **nvarchar** 類型的變數，並呼叫該變數。
+ *@input_data_1* 這是查詢所傳回的資料, 傳遞至 R 執行時間, 會將資料傳回 SQL Server 做為資料框架。
+ WITH RESULT SETS 子句會定義所傳回之資料表的架構, 以供 SQL Server, 並加入 "Hello World" 做為資料行名稱, **int**作為資料類型。

**結果**

| 世界您好 |
|-------------|
| 1 |

## <a name="next-steps"></a>後續步驟

現在您已執行幾個簡單的 R 腳本, 請仔細查看結構化輸入和輸出。

> [!div class="nextstepaction"]
> [入門處理輸入和輸出](quickstart-r-inputs-and-outputs.md)
