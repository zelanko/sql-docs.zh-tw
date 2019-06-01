---
title: 快速入門，來驗證 Python 存在於 SQL Server
description: 適用於驗證 Python 和 Machine Learning 服務存在於 SQL Server 的快速入門。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 09b96f6934fec9e24ca4a254a1d14c23327ebe5b
ms.sourcegitcommit: 944af0f6b31bf07c861ddd4d7960eb7f018be06e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66454713"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>快速入門：驗證 Python 存在於 SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 包含內建的 SQL Server 資料的資料科學分析的 Python 語言支援。 執行指令碼是透過預存程序，使用下列其中一個方法：

+ 內建[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)預存程序，將 Python 指令碼中的傳遞做為輸入參數。
+ 將 Python 指令碼中的包裝[之自訂預存程序](sqldev-in-database-r-for-sql-developers.md)您所建立。

在本快速入門中，您會確認[SQL Server 2017 Machine Learning 服務](../what-is-sql-server-machine-learning.md)已安裝和設定。

## <a name="prerequisites"></a>先決條件

這個練習需要存取之 SQL Server 執行個體[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)安裝。

您的 SQL Server 執行個體可位於 Azure 虛擬機器或內部部署。 要小心，外部指令碼功能預設為停用，因此您可能需要[啟用外部指令碼](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)，並確認**SQL Server Launchpad 服務**開始之前執行。

您也需要工具來執行 SQL 查詢。 您可以執行 Python 指令碼使用的任何資料庫管理，或查詢工具，只要它可以連線到 SQL Server 執行個體，並執行 T-SQL 查詢或預存程序。 本快速入門會使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="verify-python-exists"></a>請確認有 Python

您可以確認 （已啟用您 SQL Server 執行個體，並已安裝 Python 版本該機器學習服務。 請遵循下列步驟。

1. 開啟 SQL Server Management Studio 並連接到您的 SQL Server 執行個體。

2. 執行下列程式碼。 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. Python`print`函式會傳回的版本**訊息**視窗。 在下列範例輸出中，您所見，SQL Server 在此情況下會有 Python 安裝 3.5.2 版。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

如果您收到錯誤，有各種您可以如何確保可以通訊的執行個體和 Python 的項目。

首先，排除任何安裝問題。 若要啟用外部程式碼程式庫需要後續安裝設定。 請參閱[安裝 SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)。 同樣地，請確定 Launchpad 服務正在執行。

您也必須加入 Windows 使用者群組`SQLRUserGroup`做為登入執行個體，以確定 Launchpad 可提供 Python 和 SQL Server 之間的通訊上。 （相同的群組會用於這兩個 R 和 Python 程式碼執行）。如需詳細資訊，請參閱 < [SQLRUserGroup 建立登入](../security/create-a-login-for-sqlrusergroup.md)。

此外，您可能需要啟用網路通訊協定已停用，或開啟防火牆，以便 SQL Server 可與外部用戶端通訊。 如需詳細資訊，請參閱 <<c0> [ 疑難排解安裝](../common-issues-external-script-execution.md)。

## <a name="call-revoscalepy-functions"></a>呼叫 revoscalepy 函式

若要確認**revoscalepy**可供使用，執行包含的範例指令碼[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)產生統計摘要資料。 下列指令碼會示範如何從內建的範例包含在 revoscalepy 擷取範例.xdf 資料檔案。 RxOptions 函式會提供**sampleDataDir**傳回的範例檔案位置的參數。

因為 rx_summary 傳回型別的物件`class revoscalepy.functions.RxSummary.RxSummaryResults`，其中包含多個項目，您可以使用 pandas 資料框架以表格格式中擷取。

```sql
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

## <a name="list-python-packages"></a>清單中的 Python 套件

Microsoft 提供的預先安裝在您的 SQL Server 執行個體的 使用機器學習服務的 Python 套件的數目。 若要查看的清單的哪一個 Python 安裝套件，包括版本，遵循下列步驟。

1. 在您的 SQL Server 執行個體上執行下列指令碼。

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. 輸出是來自`pip.get_installed_distributions()`在 Python 中及當做傳回`STDOUT`訊息。

    **結果**

    ```text
    STDOUT message(s) from external script: 
    xlwt 1.2.0
    XlsxWriter 0.9.6
    xlrd 1.0.0
    win-unicode-console 0.5
    widgetsnbextension 2.0.0
    wheel 0.29.0
    Werkzeug 0.12.1
    wcwidth 0.1.7
    unicodecsv 0.14.1
    traitlets 4.3.2
    tornado 4.4.2
    toolz 0.8.2
    testpath 0.3
    tables 3.2.2
    sympy 1.0
    statsmodels 0.8.0
    sqlparse 0.1.19
    SQLAlchemy 1.1.9
    snowballstemmer 1.2.1
    six 1.10.0
    simplegeneric 0.8.1
    seaborn 0.7.1
    scipy 0.19.0
    scikit-learn 0.18.1
    ...
    ```

## <a name="next-steps"></a>後續步驟

現在您已確認您的執行個體已準備好使用 Python，看看基本的 Python 互動。

> [!div class="nextstepaction"]
> [快速入門：SQL Server 中的"Hello world"Python 指令碼](quickstart-python-run-using-t-sql.md)
