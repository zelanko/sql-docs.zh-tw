---
title: 在 T-sql 中執行「Hello World」基本 Python 程式碼的快速入門
description: SQL Server 中 Python 腳本的快速入門。 瞭解在 hello world 練習中使用 sp_execute_external_script 系統預存程式來呼叫 Python 腳本的基本概念。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/10/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: caa462fa6449d4d130ace629f99c8061c7b8a35f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345493"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>快速入門：SQL Server 中的 "Hello world" Python 腳本 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入門中, 您可以藉由執行「Hello World」 Python 腳本 inT-SQL 來瞭解重要概念, 其中包含**sp_execute_external_script**系統預存程式的簡介。 

## <a name="prerequisites"></a>必要條件

先前的快速入門中, 請[確認 Python 存在於 SQL Server](quickstart-python-verify.md)中, 提供設定本快速入門所需之 python 環境的相關資訊和連結。

## <a name="basic-python-interaction"></a>基本 Python 互動

在 SQL Server 中執行 Python 程式碼的方式有兩種:

+ 將 Python 腳本新增為系統預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的引數。

+ 從[遠端 Python 用戶端](../python/setup-python-client-tools-sql.md), 連接到 SQL Server, 然後使用 SQL Server 作為計算內容來執行程式碼。 這需要[revoscalepy](../python/ref-py-revoscalepy.md)。

下列練習著重于第一個互動模型: 如何將 Python 程式碼傳遞至預存程式。

1. 執行一些簡單的程式碼, 以瞭解如何在 SQL Server 與 Python 之間來回傳遞資料。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. 假設您已正確設定所有專案, 而且 python 和 SQL Server 彼此交談, 則會計算正確的結果, 且 python `print`函式會將結果傳回至 [**訊息**] 視窗。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    在測試您的程式碼時, 取得**stdout**訊息很方便, 但您通常需要以表格格式傳回結果, 以便在應用程式中使用它或將其寫入資料表。

現在請記住這些規則:

+ 引數內`@script`的所有專案都必須是有效的 Python 程式碼。 
+ 程式碼必須遵循所有有關縮排、變數名稱等等的 Python 規則。 當您收到錯誤時, 請檢查您的空白字元和大小寫。
+ 在程式設計語言中, Python 是一種最具彈性的單引號, 與雙引號相對,它們很容易互換。 不過, t-sql 只會針對特定專案使用單引號, 而`@script`引數會使用單引號來括住 Python 程式碼, 以做為 Unicode 字串。 因此, 您可能需要檢查 Python 程式碼, 並將一些單引號變更為雙引號。
+ 如果您使用預設未載入的任何程式庫, 您必須在腳本開頭使用 import 語句來載入它們。 SQL Server 新增數個產品特定的程式庫。 如需詳細資訊, 請參閱[Python 程式庫](../python/python-libraries-and-data-types.md)。
+ 如果尚未安裝程式庫, 請在 SQL Server 外部停止並安裝 Python 套件, 如下所述:[在 SQL Server 上安裝新的 Python 套件](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>執行 Hello World 腳本

下列練習會執行另一個簡單的 Python 腳本。

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

此預存程式的輸入包括:

+ *@language* 參數會定義要呼叫的語言擴充功能, 在此案例中為 Python。
+ *@script* 參數會定義傳遞至 Python 執行時間的命令。 您的整個 Python 腳本必須以 Unicode 文字的形式包含在此引數中。 您也可以將文字新增至 **nvarchar** 類型的變數，並呼叫該變數。
+ *@input_data_1* 這是查詢所傳回的資料, 傳遞至 Python 執行時間, 會將資料傳回 SQL Server 做為資料框架。
+ WITH RESULT SETS 子句會定義所傳回之資料表的架構, 以供 SQL Server, 並加入 "Hello World" 做為資料行名稱, **int**作為資料類型。

**結果**

| 世界您好 |
|-------------|
| 1 |

## <a name="next-steps"></a>後續步驟

現在您已執行幾個簡單的 Python 腳本, 請仔細查看結構化輸入和輸出。

> [!div class="nextstepaction"]
> [入門處理輸入和輸出](quickstart-python-inputs-and-outputs.md)
