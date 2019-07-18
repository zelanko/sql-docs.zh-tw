---
title: Python 程式設計語言擴充功能-SQL Server Machine Learning
description: 了解執行 Python 程式碼和 SQL Server 2017 Machine Learning 服務中的內建 Python 程式庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: abf7028c8b55f4f97770586f2a678a538f01b29a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963046"
---
# <a name="python-language-extension-in-sql-server"></a>SQL Server 中的 Python 語言擴充功能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用 Python 擴充功能是以關聯式資料庫引擎的 SQL Server Machine Learning 服務附加元件的一部分。 它會新增 Python 執行環境中，使用 Python 3.5 執行階段和解譯器，標準程式庫與工具，以及 Microsoft 的產品程式庫適用於 Python 的 Anaconda 散發套件： [revoscalepy](../python/ref-py-revoscalepy.md)分析在規模及[microsoftml](../python/ref-py-microsoftml.md)機器學習服務演算法。 

Python 整合安裝成[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)。

安裝 Python 3.5 執行階段和解譯器可確保使用標準 Python 解決方案近乎完整的相容性。 從 SQL Server，以確保不影響資料庫作業，在不同的處理序中執行 Python。

## <a name="python-components"></a>Python 元件

SQL Server 包含開放原始碼和專屬套件。 安裝程式所安裝的 Python 執行階段是使用 Python 3.5 的 Anaconda 4.2。 Python 執行階段安裝獨立於 SQL 工具和外部核心引擎的程序，在擴充性架構中執行。 使用 Python 的 Machine Learning 服務的安裝的一部分，您必須同意 GNU 公用授權條款。 

SQL Server 不會修改 Python 可執行檔，但您必須使用的安裝程式安裝，因為該版本是專屬的套件，建置及測試上的 Python 版本。 Anaconda 散發套件所支援的套件清單，請參閱 Continuum analytics 網站：[Anaconda 套件清單](https://docs.continuum.io/anaconda/packages/pkg-docs)。

執行個體相關聯的資料夾中，可以找到與特定資料庫引擎執行個體相關聯的 Anaconda 散發套件。 例如，如果您使用 Machine Learning 服務與 Python 安裝 SQL Server 2017 資料庫引擎的預設執行個體時，查看底下`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`。

Python 套件的平行和分散式工作負載，Microsoft 將加入包含下列的程式庫。

| 程式庫 | 描述 |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 支援資料來源物件和資料探索、 操作、 轉換和視覺效果。 它支援建立遠端計算內容，以及各種不同的可調整機器學習服務模型，例如**rxLinMod**。 如需詳細資訊，請參閱 < [revoscalepy 模組與 SQL Server](../python/ref-py-revoscalepy.md)。  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 包含已針對速度及準確性，最佳化，以及內嵌轉換處理文字與映像的機器學習演算法。 如需詳細資訊，請參閱 < [microsoftml 模組與 SQL Server](../python/ref-py-microsoftml.md)。 |

緊密結合 Microsoftml 和 revoscalepy;使用 microsoftml 中的資料來源定義為 revoscalepy 物件。 計算 microsoftml revoscalepy 傳輸中的內容限制。 也就是所有功能都都可供本機作業，但切換至遠端計算內容需要 RxInSqlServer。

## <a name="using-python-in-sql-server"></a>SQL Server 中使用 Python

您匯入**revoscalepy**模組到您的 Python 程式碼，然後呼叫函式，從模組，例如任何其他的 Python 函式。

支援的資料來源包含 ODBC 資料庫、 SQL Server 與 XDF 檔案格式交換資料與其他來源，或使用 R 解決方案。 適用於 Python 的輸入的資料必須是表格式。 所有 Python 結果必須都傳回的形式**pandas**資料框架。

支援的計算內容包括本機或遠端 SQL Server 計算內容。 在遠端計算內容是指在工作站上，例如一部電腦啟動的程式碼執行，但參數然後指令碼到遠端電腦的執行。 切換計算內容時，需要兩個系統都有相同的 revoscalepy 程式庫。

本機計算內容，如您所料，包括資料庫引擎執行個體，與相同的伺服器上使用 T-SQL 程式碼的 Python 程式碼的執行，或內嵌在預存程序。 您也可以從本機 Python IDE 執行程式碼，並可在 SQL Server 電腦上執行，藉由定義遠端計算內容的指令碼。

## <a name="execution-architecture"></a>執行架構

下列圖表描述與每個支援的案例中的 Python 執行階段 SQL Server 元件的互動： 從 Python 終端機中，使用 SQL Server 計算內容中執行指令碼在資料庫和遠端執行。

### <a name="python-scripts-executed-in-database"></a>執行資料庫中的 Python 指令碼

當您執行 「 內部 」 SQL Server 的 Python 時，您必須封裝在特殊的預存程序中，Python 指令碼[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

指令碼已經內嵌在預存程序之後，可以進行呼叫的預存程序的任何應用程式可以起始執行 Python 程式碼。  SQL Server 之後可以管理執行程式碼以在下圖摘要說明。

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Python 執行階段的要求會由參數`@language='Python'`傳遞至預存程序。 SQL Server 會將此要求傳送到 Launchpad 服務。
2. Launchpad 服務啟動適當的啟動器;在此情況下，PythonLauncher。
3. PythonLauncher 啟動外部 Python35 程序。
4. BxlServer 會協調與管理交換資料，以及處理結果的儲存體的 Python 執行階段。
5. SQL Satellite 管理相關的工作和程序與 SQL Server 的通訊。
6. BxlServer 使用 SQL Satellite 來傳達狀態，以及 SQL Server 的結果。
7. SQL Server 取得結果，並關閉相關的工作和程序。

### <a name="python-scripts-executed-from-a-remote-client"></a>從遠端用戶端執行的 Python 指令碼

您可以從遠端電腦，例如膝上型電腦，執行 Python 指令碼，並讓它們在 SQl Server 電腦的內容中執行，如果符合這些條件：

+ 您適當地設計指令碼
+ 在遠端電腦已安裝 Machine Learning 服務所使用的擴充性程式庫。 [Revoscalepy](../python/ref-py-revoscalepy.md)封裝，才能使用遠端計算內容。

下圖摘要說明整體的工作流程時指令碼會從遠端電腦。

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. 中支援的函式**revoscalepy**，Python 執行階段呼叫連結的函式，再進而呼叫 BxlServer。
2. BxlServer 隨附 Machine Learning 服務 （資料庫），並以個別的處理序執行來自 Python 執行階段。
3. BxlServer 會判斷連線目標，並啟始連線使用 ODBC，傳遞做為 Python 指令碼中的連接字串的一部分提供的認證。
4. BxlServer 開啟 SQL Server 執行個體的連接。
5. 當呼叫的外部指令碼執行階段時，Launchpad 服務會叫用，其接著會啟動適當的啟動器： 在此情況下，PythonLauncher.dll。 之後，將處理的 Python 程式碼處理類似於工作流程中，在 T-SQL 中的預存程序叫用 Python 程式碼時。
6. PythonLauncher 可呼叫的執行個體的 SQL Server 電腦安裝 Python。
7. 結果會傳回 BxlServer。
8. SQL Satellite 管理與 SQL Server 與清除作業相關的工作物件的通訊。
9. SQL Server 會將結果傳遞回用戶端。

## <a name="see-also"></a>另請參閱

+ [SQL Server 中的 revoscalepy 模組](../python/ref-py-revoscalepy.md)
+ [revoscalepy 函式參考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [SQL Server 中的擴充性架構](extensibility-framework.md)
+ [R 和機器學習服務在 SQL Server 中的延伸模組](extension-r.md)