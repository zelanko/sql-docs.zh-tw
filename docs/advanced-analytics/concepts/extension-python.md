---
title: Python 程式設計語言延伸模組
description: 瞭解 SQL Server Machine Learning Services 中的 Python 程式碼執行和內建 Python 程式庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f3825a2b5085bf5a6e144a602c36cb20ccaca430
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688287"
---
# <a name="python-language-extension-in-sql-server"></a>SQL Server 中的 Python 語言延伸模組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Python 延伸模組是關係資料庫引擎之 SQL Server Machine Learning 服務附加元件的一部分。 它會新增 Python 執行環境、Anaconda 散發與 Python 3.5 執行時間和解譯器、標準程式庫和工具, 以及適用于 Python 的 Microsoft 產品程式庫: 適用于大規模分析的[revoscalepy](../python/ref-py-revoscalepy.md)和[microsoftml](../python/ref-py-microsoftml.md)機器學習演算法。 

Python 整合會安裝為[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)。

安裝 Python 3.5 執行時間和解譯器可確保與標準 Python 解決方案幾乎完全相容。 Python 會在與 SQL Server 不同的進程中執行, 以確保資料庫作業不會受到危害。

## <a name="python-components"></a>Python 元件

SQL Server 包含開放原始碼和專屬的套件。 安裝程式所安裝的 Python 執行時間是 Anaconda 4.2 與 Python 3.5。 Python 執行時間是獨立安裝的 SQL 工具, 而且是在擴充性架構中的核心引擎進程外部執行。 在使用 Python 安裝 Machine Learning 服務的過程中, 您必須同意 GNU 公開授權的條款。 

SQL Server 不會修改 Python 可執行檔, 但您必須使用安裝程式所安裝的 Python 版本, 因為該版本是專屬套件的建立和測試者。 如需 Anaconda 發佈所支援的套件清單, 請參閱 Continuum analytics 網站:[Anaconda 封裝清單](https://docs.continuum.io/anaconda/packages/pkg-docs)。

與特定資料庫引擎實例相關聯的 Anaconda 散發, 可以在與實例相關聯的資料夾中找到。 例如, 如果您在預設實例上使用 Machine Learning Services 和 Python 安裝 SQL Server 2017 資料庫引擎, 請查看`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`。

Microsoft 為平行和分散式工作負載新增的 Python 套件包含下列程式庫。

| 程式庫 | 描述 |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 支援資料來源物件和資料探索、操作、轉換和視覺化。 它支援建立遠端計算內容, 以及各種可調整的機器學習模型, 例如**rxLinMod**。 如需詳細資訊, 請參閱[具有 SQL Server 的 revoscalepy 模組](../python/ref-py-revoscalepy.md)。  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 包含已針對速度和精確度優化的機器學習演算法, 以及使用文字和影像的內嵌轉換。 如需詳細資訊, 請參閱[具有 SQL Server 的 microsoftml 模組](../python/ref-py-microsoftml.md)。 |

Microsoftml 和 revoscalepy 緊密結合;microsoftml 中使用的資料來源會定義為 revoscalepy 物件。 Revoscalepy 傳送至 microsoftml 的計算內容限制。 也就是說, 所有功能都可供本機作業使用, 但切換到遠端計算內容需要 RxInSqlServer。

## <a name="using-python-in-sql-server"></a>在 SQL Server 中使用 Python

您會將**revoscalepy**模組匯入 Python 程式碼, 然後從模組呼叫函式, 就像任何其他 Python 函式一樣。

支援的資料來源包括 ODBC 資料庫、SQL Server 和 XDF 檔案格式, 以與其他來源或 R 解決方案交換資料。 Python 的輸入資料必須是表格式。 所有的 Python 結果都必須以**pandas**資料框架的形式傳回。

支援的計算內容包括本機或遠端 SQL Server 計算內容。 遠端計算內容是指在一部電腦 (例如工作站) 上啟動的程式碼執行, 但接著會將腳本執行切換至遠端電腦。 若要切換計算內容, 這兩個系統都需要有相同的 revoscalepy 程式庫。

如您所預期, 本機計算內容包含在與 database engine 實例相同的伺服器上執行 Python 程式碼, 並在 T-sql 或內嵌于預存程式中。 您也可以藉由定義遠端計算內容, 從本機 Python IDE 執行程式碼, 並在 SQL Server 電腦上執行腳本。

## <a name="execution-architecture"></a>執行架構

下圖說明在每個支援的案例中, SQL Server 元件與 Python 執行時間的互動: 使用 SQL Server 的計算內容, 在資料庫中執行腳本, 以及從 Python 終端機遠端執行。

### <a name="python-scripts-executed-in-database"></a>在資料庫內執行的 Python 腳本

當您執行 Python 「內部」 SQL Server 時，您必須將 Python 腳本封裝在特殊的預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)中。

將腳本內嵌在預存程式中之後, 任何可進行預存程序呼叫的應用程式都可以起始 Python 程式碼的執行。  之後 SQL Server 會依照下圖中的摘要來管理程式碼執行。

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Python 執行時間的要求是由傳遞至預存`@language='Python'`程式的參數所表示。 SQL Server 會將此要求傳送至啟動列服務。
2. 啟動列服務會啟動適當的啟動程式;在此情況下, 請 PythonLauncher。
3. PythonLauncher 會啟動外部 Python35 進程。
4. BxlServer 會與 Python 執行時間協調, 以管理資料的交換, 以及儲存工作結果。
5. SQL 附屬作業會使用 SQL Server 來管理相關工作和進程的通訊。
6. BxlServer 會使用 SQL 附屬來傳達狀態和結果, 以 SQL Server。
7. SQL Server 會取得結果, 並關閉相關的工作和進程。

### <a name="python-scripts-executed-from-a-remote-client"></a>從遠端用戶端執行的 Python 腳本

您可以從遠端電腦 (例如膝上型電腦) 執行 Python 腳本, 並讓它們在 SQl Server 電腦的內容中執行 (如果符合這些條件的話):

+ 您會適當地設計腳本
+ 遠端電腦已安裝 Machine Learning 服務所使用的擴充性程式庫。 需要[revoscalepy](../python/ref-py-revoscalepy.md)封裝, 才能使用遠端計算內容。

下圖摘要說明從遠端電腦傳送腳本時的整體工作流程。

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. 針對**revoscalepy**中支援的函式, Python 執行時間會呼叫連結函式, 而該函式會接著呼叫 BxlServer。
2. BxlServer 隨附于 Machine Learning 服務 (資料庫內), 而且會在 Python 執行時間的個別進程中執行。
3. BxlServer 會判斷連接目標, 並使用 ODBC 起始連接, 並在 Python 腳本中傳遞當做連接字串一部分提供的認證。
4. BxlServer 會開啟 SQL Server 實例的連接。
5. 呼叫外部腳本執行時間時, 會叫用啟動列服務, 而這會接著啟動適當的啟動程式: 在此案例中為 PythonLauncher。 之後, 當從 T-sql 中的預存程式叫用 Python 程式碼時, 就會在類似的工作流程中處理 Python 程式碼的處理。
6. PythonLauncher 會呼叫安裝在 SQL Server 電腦上的 Python 實例。
7. 結果會傳回 BxlServer。
8. SQL 衛星管理與 SQL Server 和清除相關工作物件的通訊。
9. SQL Server 會將結果傳回到用戶端。

## <a name="next-steps"></a>後續步驟

+ [SQL Server 中的 revoscalepy 模組](../python/ref-py-revoscalepy.md)
+ [revoscalepy 函數參考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [SQL Server 中的擴充性架構](extensibility-framework.md)
+ [SQL Server 中的 R 和機器學習擴充功能](extension-r.md)
+ [取得 Python 套件資訊](../package-management/python-package-information.md)
+ [使用 sqlmlutils 安裝 Python 套件](../package-management/install-additional-python-packages-on-sql-server.md)
