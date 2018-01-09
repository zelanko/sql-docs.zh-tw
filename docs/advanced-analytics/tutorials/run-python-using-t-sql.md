---
title: "執行 Python 使用 T-SQL |Microsoft 文件"
ms.custom: 
ms.date: 09/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: Python
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 6b481e5e65616f70f1b66c9be2517a2da747b1dd
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="run-python-using-t-sql"></a>執行 Python 使用 T-SQL

這個範例會示範如何使用預存程序在 SQL Server 中，執行簡單的 Python 指令碼[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

## <a name="step-1-create-the-test-data-table"></a>步驟 1： 建立測試資料表

首先，您將建立一些額外的資料，若要使用的來源資料對應的星期名稱時。 執行下列 T-SQL 陳述式來建立資料表。

```SQL
CREATE TABLE PythonTest (
    [DayOfWeek] varchar(10) NOT NULL,
    [Amount] float NOT NULL
    )
GO

INSERT INTO PythonTest VALUES
('Sunday', 10.0),
('Monday', 11.1),
('Tuesday', 12.2),
('Wednesday', 13.3),
('Thursday', 14.4),
('Friday', 15.5),
('Saturday', 16.6),
('Friday', 17.7),
('Monday', 18.8),
('Sunday', 19.9)
GO
```

## <a name="step-2-run-the-hello-world-script"></a>步驟 2： 執行"Hello World"指令碼

下列程式碼載入 Python 可執行檔、 將傳遞的輸入的資料，並針對每個輸入資料列，更新資料表中的日期名稱以數字代表一週的索引。

記下參數的 *@RowsPerRead* 。 這個參數會指定傳遞至 Python 執行階段從 SQL Server 的資料列數目。

Python 資料分析程式庫，又稱為**熊**，需要將資料傳遞至 SQL Server，以及包含根據預設，使用機器學習服務。

```sql
DECLARE @ParamINT INT = 1234567
DECLARE @ParamCharN VARCHAR(6) = 'INPUT '

print '------------------------------------------------------------------------'
print 'Output parameters (before):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)

print 'Dataset (before):'
SELECT * FROM PythonTest

print '------------------------------------------------------------------------'
print 'Dataset (after):'
DECLARE @RowsPerRead INT = 5

execute sp_execute_external_script 
@language = N'Python',
@script = N'
import sys
import os
print("*******************************")
print(sys.version)
print("Hello World")
print(os.getcwd())
print("*******************************")
if ParamINT == 1234567:
       ParamINT = 1
else:
       ParamINT += 1

ParamCharN="OUTPUT"
OutputDataSet = InputDataSet

global daysMap

daysMap = {
       "Monday" : 1,
       "Tuesday" : 2,
       "Wednesday" : 3,
       "Thursday" : 4,
       "Friday" : 5,
       "Saturday" : 6,
       "Sunday" : 7
       }

OutputDataSet["DayOfWeek"] = pandas.Series([daysMap[i] for i in OutputDataSet["DayOfWeek"]], index = OutputDataSet.index, dtype = "int32")
', 
@input_data_1 = N'SELECT * FROM PythonTest', 
@params = N'@r_rowsPerRead INT, @ParamINT INT OUTPUT, @ParamCharN CHAR(6) OUTPUT',
@r_rowsPerRead = @RowsPerRead,
@paramINT = @ParamINT OUTPUT,
@paramCharN = @ParamCharN OUTPUT
with result sets (("DayOfWeek" int null, "Amount" float null))

print 'Output parameters (after):'
print FORMATMESSAGE('ParamINT=%d', @ParamINT)
print FORMATMESSAGE('ParamCharN=%s', @ParamCharN)
GO
```

> [!TIP]
> 本快速入門的詳細說明此預存程序的參數： [T-SQL 中的使用 R 程式碼](rtsql-using-r-code-in-transact-sql-quickstart.md)。

## <a name="step-3-view-the-results"></a>步驟 3： 檢視結果

預存程序取得原始資料、 套用 Python 指令碼，然後傳回 中修改的資料**結果**Management Studio 或其他 SQL 查詢工具窗格。


|DayOfWeek （之前）| Amount|DayOfWeek （之後） |
|-----|-----|-----|
|星期日|10|7|
|星期一|11.1|@shouldalert|
|星期二|12.2|2|
|星期三|13.3|3|
|星期四|14.4|4|
|星期五|15.5|5|
|星期六|16.6|6|
|星期五|17.7|5|
|星期一|18.8|@shouldalert|
|星期日|19.9|7|

狀態訊息 」 或 「 錯誤傳回至 Python 主控台會以訊息中傳回**查詢**視窗。 以下是摘錄，您可能會看到的輸出：

*範例結果*

```
Output parameters (before):
ParamINT=1234567
ParamCharN=INPUT 
Dataset (before):

(10 rows affected)

Dataset (after):
STDOUT message(s) from external script: 
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

3.5.2 |Anaconda 4.2.0 (64-bit)| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
Hello World
C:\PROGRA~1\MICROS~2\MSSQL1~1.MSS\MSSQL\EXTENS~1\MSSQLSERVER01\7A70B3FB-FBA2-4C52-96D6-8634DB843229

(10 rows affected)
Output parameters (after):
ParamINT=2
ParamCharN=OUTPUT
```

+ **訊息**輸出包含指令碼執行時使用的工作目錄。 在此範例中，MSSQLSERVER01 是指 SQL Server 來管理工作所配置的背景工作帳戶。 

    GUID 是建立來儲存資料和指令碼的成品的指令碼執行期間的暫存資料夾的名稱。 這些暫存資料夾受保護的 SQL Server，而由 Windows 作業物件之後清除指令碼已終止。

+ 包含"Hello World"訊息區段會列印兩次。 這是因為值 *@RowsPerRead* 已設定為 5 並在資料表中有 10 個資料列; 因此，Python 的兩個呼叫會需要處理資料表中的所有資料列。

    在實際執行時，我們建議您試驗不同的值，以判斷應該在每個批次中傳遞的資料列的數目上限。 最佳的資料列數目與相關資料，並受到集中的資料行數目和您要傳遞的資料類型。

## <a name="resources"></a>資源

請參閱這些其他的 Python 範例和進階的秘訣和示範端對端教學課程。

+ [若要建立的模型使用 Python revoscalepy](use-python-revoscalepy-to-create-model.md)
+ [資料庫中的 SQL 開發人員的 Python](sqldev-in-database-python-for-sql-developers.md)
+ [建置預測模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

## <a name="troubleshooting"></a>疑難排解

如果找不到預存程序， `sp_execute_external_script`，這表示您可能尚未完成設定要支援外部指令碼執行的執行個體。 執行 SQL Server 2017 安裝程式並選取後 Python 和機器學習語言，您必須同時也可以明確啟用功能使用`sp_configure`，然後重新啟動執行個體。 如需詳細資訊，請參閱[安裝程式的機器學習服務使用 Python](../python/setup-python-machine-learning-services.md)。