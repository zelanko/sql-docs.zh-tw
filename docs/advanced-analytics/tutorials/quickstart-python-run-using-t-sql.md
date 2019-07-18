---
title: 快速入門中的"Hello World"基本的 Python 程式碼在 T-SQL-SQL Server Machine Learning 中執行
description: 適用於 SQL Server 中的 Python 指令碼的快速入門。 了解呼叫 Python 指令碼在 hello world 練習使用 sp_execute_external_script 的系統預存程序的基本概念。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/10/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: a2d0987441f8f26304590f5ccbde15a2e15cf3c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962060"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>快速入門：SQL Server 中的"Hello world"Python 指令碼 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入門中，您將了解重要的概念，透過執行"Hello World"Python 指令碼 inT SQL，簡介**sp_execute_external_script**系統預存程序。 

## <a name="prerequisites"></a>先決條件

先前的快速入門中，[確認 Python 存在於 SQL Server](quickstart-python-verify.md)，提供資訊並連結設定本快速入門所需的 Python 環境。

## <a name="basic-python-interaction"></a>Python 的基本互動

有兩種方式可在 SQL Server 中執行 Python 程式碼：

+ 做為引數的系統預存程序中，新增 Python 指令碼[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 從[遠端 Python 用戶端](../python/setup-python-client-tools-sql.md)、 連接到 SQL Server 和執行程式碼使用 SQL Server 作為計算內容。 這需要[revoscalepy](../python/ref-py-revoscalepy.md)。

下列練習著重於第一次的互動模型： 如何將 Python 程式碼傳遞至預存程序。

1. 執行一些簡單的程式碼，以查看資料的 SQL Server 與 Python 之間的來回傳遞方式。

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

2. 假設您有正確設定的所有項目，以及 Python 和 SQL Server 與彼此通訊，正確的結果計算，和 Python`print`函式會傳回結果**訊息**windows。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    取得時發生**stdout**測試您的程式碼時，訊息是好用，通常您需要以表格式格式傳回結果，以便您可以在應用程式中使用它，或寫入資料表。

現在，請記住這些規則：

+ 所有東西放在`@script`引數必須是有效的 Python 程式碼。 
+ 程式碼必須遵循有關縮排、 變數名稱，以及其他等等的所有 Python 規則。 當您收到錯誤時，請檢查您的泛空白字元和大小寫。
+ 在程式設計語言，Python 是其中一個最具彈性方面單引號與雙引號括住;它們幾乎可以互換。 不過，T-SQL 會使用單引號來某些事，而`@script`引數會使用單引號來括住的 Unicode 字串的 Python 程式碼。 因此，您可能需要檢閱您的 Python 程式碼，並將一些單引號變更為雙引號括住。
+ 如果您使用預設不會載入任何程式庫，您必須在您的指令碼開頭使用匯入陳述式，載入它們。 SQL Server 將新增多個產品專屬程式庫。 如需詳細資訊，請參閱 < [Python 程式庫](../python/python-libraries-and-data-types.md)。
+ 如果尚未安裝的程式庫，請停止並安裝 SQL Server 外部 Python 套件，如下所示：[在 SQL Server 上安裝新的 Python 套件](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>執行 Hello World 指令碼

下列練習中執行另一個簡單的 Python 指令碼。

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

這個預存程序的輸入包括：

+ *@language* 參數會定義要呼叫，在此情況下，Python 語言擴充功能。
+ *@script* 參數會定義傳遞至 Python 執行階段的命令。 您完整的 Python 指令碼必須括住這個引數，成為 Unicode 文字。 您也可以將文字新增至 **nvarchar** 類型的變數，並呼叫該變數。
+ *@input_data_1* 會傳回查詢所傳遞至 Python 執行階段，將資料傳回給 SQL Server 做為資料框架的資料。
+ 結果集子句會定義傳回的資料表的結構描述 SQL Server，將"Hello World"新增為資料行名稱，如**int**資料類型。

**結果**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>後續步驟

現在您已經執行數個簡單的 Python 指令碼，看看建構輸入和輸出。

> [!div class="nextstepaction"]
> [快速入門：處理輸入和輸出](quickstart-python-inputs-and-outputs.md)
