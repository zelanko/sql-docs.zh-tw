---
title: Python 程式設計語言延伸模組
description: 了解 SQL Server Machine Learning 服務中的 Python 程式碼執行和內建 Python 程式庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b1ada7d78cdacb88356b2148475e07d559f4ecbb
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532642"
---
# <a name="python-language-extension-in-sql-server"></a>SQL Server 中的 Python 語言延伸模組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Python 延伸模組是 SQL Server 機器學習服務對關聯式資料庫引擎的附加元件之一。 該延伸模組會新增 Python 執行環境、Anaconda 散發與 Python 3.5 執行時間和解譯器、標準程式庫和工具，以及適用於 Python 的 Microsoft 產品程式庫：適用於大規模分析的 [revoscalepy](../python/ref-py-revoscalepy.md) 以及適用於機器學習演算法的 [microsoftml](../python/ref-py-microsoftml.md)。 

Python 整合會安裝為 [SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)。

安裝 Python 3.5 執行階段和解譯器可確保與標準 Python 解決方案幾乎完全相容。 Python 會在與 SQL Server 不同的程序中執行，以確保資料庫作業不會受到危害。

## <a name="python-components"></a>Python 元件

SQL Server 包含開放原始碼和專屬套件。 安裝程式所安裝的 Python 執行階段是 Anaconda 4.2 與 Python 3.5。 Python 執行階段是獨立安裝的 SQL 工具，並在擴充性架構中的核心引擎處理序外部執行。 在安裝包含 Python 的 Machine Learning 服務期間，您必須同意 GNU 公用授權的條款。 

SQL Server 不會修改 Python 可執行檔，但您必須使用安裝程式所安裝的 Python 版本，因為該版本是專屬套件據以建立和測試的版本。 如需 Anaconda 發佈所支援的套件清單，請參閱 Continuum Analytics 網站：[Anaconda 套件清單](https://docs.continuum.io/anaconda/packages/pkg-docs)。

與特定資料庫引擎執行個體建立關聯的 Anaconda 散發，可以在與該執行個體建立關聯的資料夾中找到。 例如，如果您已在預設執行個體上使用 Machine Learning 服務和 Python 安裝 SQL Server 2017 資料庫引擎，請查看 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`。

Microsoft 為平行和分散式工作負載新增的 Python 套件包含下列程式庫。

| 程式庫 | Description |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 支援資料來源物件和資料探索、操作、轉換和視覺化。 RevoScaleR 支援建立遠端計算內容，以及各種可調整的機器學習模型，例如 **rxLinMod**。 如需詳細資訊，請參閱 [revoscalepy 模組與 SQL Server](../python/ref-py-revoscalepy.md)。  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 包含已針對速度和正確性最佳化的機器學習演算法，以及適用於處理文字和影像的內嵌轉換。 如需詳細資訊，請參閱 [microsoftml 模組與 SQL Server](../python/ref-py-microsoftml.md)。 |

Microsoftml 和 revoscalepy 緊密結合；在 microsoftml 中使用的資料來源會定義為 revoscalepy 物件。 Revoscalepy 傳送至 microsoftml 的計算內容限制。 也就是說，所有功能都可供本機作業使用，但切換到遠端計算內容需要 RxInSqlServer。

## <a name="using-python-in-sql-server"></a>在 SQL Server 中使用 Python

您會將 **revoscalepy** 模組匯入 Python 程式碼，然後從模組呼叫函式，就像任何其他 Python 函式一樣。

系統支援 ODBC 資料庫、SQL Server 和 XDF 檔案格式等資料來源，以便與其他來源或 R 解決方案交換資料。 Python 的輸入資料必須是表格式。 所有 Python 結果都必須以 **pandas** 資料框架的形式傳回。

支援的計算內容包括本機或遠端 SQL Server 計算內容。 遠端計算內容是指在某一部電腦 (例如工作站) 上啟動的程式碼執行，但接著將指令碼執行切換至遠端電腦的情況。 若要切換計算內容，這兩個系統都需要具備相同的 revoscalepy 程式庫。

如您所預期，本機計算內容會執行位於資料庫引擎執行個體所在相同伺服器上的 Python 程式碼，以及 T-SQL 內部或內嵌於預存程序中的程式碼。 您也可以定義遠端計算內容，以從本機 Python IDE 執行程式碼，並在 SQL Server 電腦上執行指令碼。

## <a name="execution-architecture"></a>執行架構

下圖說明在每個支援案例中，SQL Server 元件與 Python 執行階段的互動情況：使用 SQL Server 計算內容、在資料庫中執行指令碼，以及從 Python 終端機遠端執行。

### <a name="python-scripts-executed-in-database"></a>在資料庫內執行的 Python 指令碼

當執行 Python「內部」SQL Server 時，您必須將 Python 指令碼封裝在特殊的預存程序中，[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

將指令碼內嵌在預存程序中之後，任何可進行預存程序呼叫的應用程式都可以起始 Python 程式碼的執行。  之後，SQL Server 會依下圖摘要說明的方式來管理程式碼執行。

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Python 執行階段的要求是由傳遞至預存程序的 `@language='Python'` 參數所表示。 SQL Server 會將此要求傳送到啟動控制板服務。
在 Linux 中，SQL 會使用**啟動控制板**服務來與每個使用者的不同啟動控制板程序通訊。 如需詳細資料，請參閱[擴充性架構圖表](extensibility-framework.md#architecture-diagram)。
2. 啟動控制板服務會啟動適當的啟動器，在此案例中為 PythonLauncher。
3. PythonLauncher 會啟動外部 Python35 程序。
4. BxlServer 會與 Python 執行階段合作，以管理資料交換，以及處理結果的儲存。
5. SQL Satellite 會管理與 SQL Server 之間相關工作和處理序的通訊。
6. BxlServer 會使用 SQL Satellite 來與 SQL Server 進行狀態和結果的通訊。
7. SQL Server 會取得結果，並關閉相關工作和處理序。

### <a name="python-scripts-executed-from-a-remote-client"></a>從遠端用戶端執行的 Python 指令碼

您可以從遠端電腦 (例如膝上型電腦) 執行 Python 指令碼，並讓這些指令碼在 SQl Server 電腦的內容中執行 (如果符合這些條件)：

+ 請適當地設計指令碼
+ 遠端電腦已安裝 Machine Learning 服務所使用的擴充性程式庫。 需要 [revoscalepy](../python/ref-py-revoscalepy.md) 套件，才能使用遠端計算內容。

下圖摘要說明從遠端電腦傳送指令碼時的整體工作流程。

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. 針對 **revoscalepy** 支援的函式，Python 執行階段會呼叫連結函式，而該函式會接著呼叫 BxlServer。
2. BxlServer 隨附於 Machine Learning 服務 (資料庫內)，且會在 Python 執行階段的個別程序中執行。
3. BxlServer 會判斷連線目標並使用 ODBC 初始化連線，並在 Python 指令碼中將認證作為連接字串的一部分來傳遞。
4. 由 BxlServer 開啟對 SQL Server 執行個體的連線。
5. 呼叫外部指令碼執行階段時會叫用啟動控制板服務，而這會接著啟動適當的啟動程式：在此案例中為 PythonLauncher.dll。 之後，當從 T-SQL 中的預存程序叫用 Python 程式碼時，就會在類似的工作流程中處理 Python 程式碼。
6. PythonLauncher 會呼叫安裝在 SQL Server 電腦上 Python 的執行個體。
7. 結果會傳回 BxlServer。
8. 由 SQL Satellite 管理與 SQL Server 的通訊，並清理相關的工作物件。
9. SQL Server 將結果傳回至用戶端。

## <a name="next-steps"></a>後續步驟

+ [SQL Server 中的 revoscalepy 模組](../python/ref-py-revoscalepy.md)
+ [RevoScaleR 函式參考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [SQL Server 中的擴充性架構](extensibility-framework.md)
+ [SQL Server 中的 R 和機器學習延伸模組](extension-r.md)
+ [取得 Python 套件資訊](../package-management/python-package-information.md)
+ [使用 sqlmlutils 安裝 Python 套件](../package-management/install-additional-python-packages-on-sql-server.md)
