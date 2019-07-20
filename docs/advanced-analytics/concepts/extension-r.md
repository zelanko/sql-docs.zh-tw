---
title: R 程式設計語言延伸模組
description: 瞭解 R 程式碼執行, 以及 SQL Server 2016 R Services 或 SQL Server 2017 Machine Learning 服務中的內建 R 程式庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3bf8e77cec92cde0e5a8adf4d3e1e36f1689b917
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343408"
---
# <a name="r-language-extension-in-sql-server"></a>SQL Server 中的 R 語言延伸模組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R 擴充功能是關係資料庫引擎之 SQL Server Machine Learning 服務附加元件的一部分。 它會新增 R 執行環境、使用標準程式庫和工具的基本 R 散發, 以及 Microsoft R 程式庫:適用于大規模分析的[RevoScaleR](../r/ref-r-revoscaler.md) 、用於機器學習服務演算法的[MicrosoftML](../r/ref-r-microsoftml.md) , 以及用來存取 SQL Server 中資料或 R 程式碼的其他程式庫。

從 SQL Server 2016 開始, 使用[r Services](../r/sql-server-r-services.md)的 SQL Server 中提供 r 整合, 並繼續做為[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)的一部分。

## <a name="r-components"></a>R 元件

SQL Server 包含開放原始碼和專屬的套件。 基本 R 程式庫會透過 Microsoft 的開放原始碼 R 發佈來安裝:Microsoft R Open (MRO)。 R 的目前使用者應該能夠移植其 R 程式碼, 並以外部進程的形式在 SQL Server 上執行, 只需進行一些修改即可。 MRO 是獨立安裝的 SQL 工具, 而且是在擴充性架構中的核心引擎進程外部執行。 在安裝期間, 您必須同意開放原始碼授權的條款。 之後, 您就可以在不需要進一步修改的情況下執行標準 R 套件, 就像在 R 的任何其他開放原始碼散發中一樣。 

SQL Server 不會修改基本 R 可執行檔, 但您必須使用安裝程式所安裝的 R 版本, 因為該版本是專屬套件的建立和測試者。 如需 MRO 與您可能會從 CRAN 取得的 R 基底散發有何差異的詳細資訊, 請參閱[與 r 語言的互通性和 Microsoft r 產品和功能](https://docs.microsoft.com/r-server/what-is-r-server-interoperability)。

安裝程式所安裝的 R 基底封裝散發套件, 可以在與實例相關聯的資料夾中找到。 例如, 如果您在 SQL Server 2016 預設實例上安裝 R Services, R 程式庫預設會位於此資料夾中: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`。 同樣地, 與預設實例相關聯的 R 工具預設會位於此資料夾中: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`。

Microsoft 為平行和分散式工作負載新增的 R 套件包含下列程式庫。

| 程式庫 | 描述 |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 支援資料來源物件和資料探索、操作、轉換和視覺化。 它支援建立遠端計算內容, 以及各種可調整的機器學習模型, 例如**rxLinMod**。 API 已經最佳化，可分析因過大而無法納入記憶體的資料集，以及執行分散在數個核心或處理器上的計算。 RevoScaleR 封裝也支援 XDF 檔案格式, 以便更快速地移動和儲存用於分析的資料。 XDF 格式會使用單欄式儲存體、具可攜性，且可用來從各種來源載入然後操作資料，包括文字、SPSS 或 ODBC 連線。 |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | 包含已針對速度和精確度優化的機器學習演算法, 以及使用文字和影像的內嵌轉換。 如需詳細資訊, 請參閱[SQL Server 中的 MicrosoftML](../r/ref-r-microsoftml.md)。 | 

## <a name="using-r-in-sql-server"></a>在 SQL Server 中使用 R

您可以使用基底函式編寫 R 的腳本, 但若要受益于多處理, 您必須將**RevoScaleR**和**MicrosoftML**模組匯入 R 程式碼, 然後呼叫其函式來建立以平行方式執行的模型。 
 
支援的資料來源包括 ODBC 資料庫、SQL Server 和 XDF 檔案格式, 以與其他來源或 R 解決方案交換資料。 輸入資料必須是表格式。 所有 R 結果都必須以資料框架的形式傳回。

支援的計算內容包括本機或遠端 SQL Server 計算內容。 遠端計算內容是指在一部電腦 (例如工作站) 上啟動的程式碼執行, 但接著會將腳本執行切換至遠端電腦。 若要切換計算內容, 這兩個系統都需要有相同的 RevoScaleR 程式庫。

如您所預期, 本機計算內容包含在與 database engine 實例相同的伺服器上執行 R 程式碼, 並在 T-sql 或內嵌于預存程式中。 您也可以藉由定義遠端計算內容, 從本機 R IDE 執行程式碼, 並在 SQL Server 電腦上執行腳本。

## <a name="execution-architecture"></a>執行架構

下圖說明在每個支援的案例中, SQL Server 元件與 R 執行時間的互動: 使用 SQL Server 的計算內容, 在資料庫中執行腳本, 以及從 R 命令列遠端執行。

### <a name="r-scripts-executed-from-sql-server-in-database"></a>從資料庫 SQL Server 執行的 R 腳本

從「內部」 SQL Server 執行的 R 程式碼是藉由呼叫預存程式來執行。 因此，任何可以進行預存程序呼叫的應用程式都能初始化 R 程式碼的執行。  之後 SQL Server 管理 R 程式碼的執行, 如下圖所摘要說明。

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. 對於 R 執行階段的要求會以傳遞到預存程序 ([sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)) 的參數 _@language='R'_ 表示。 SQL Server 會將此要求傳送至啟動列服務。
2. Launchpad 服務會啟動適當的啟動器，在此案例中為 RLauncher。
3. RLauncher 啟動外部 R 處理序。
4. BxlServer 會與 R 執行時間協調, 以管理資料的交換, 並 SQL Server 和儲存工作結果。
5. SQL 附屬作業會使用 SQL Server 來管理相關工作和進程的通訊。
6. BxlServer 會使用 SQL 附屬來傳達狀態和結果, 以 SQL Server。
7. SQL Server 會取得結果, 並關閉相關的工作和進程。

### <a name="r-scripts-executed-from-a-remote-client"></a>從遠端用戶端執行的 R 指令碼

從支援 Microsoft R 的遠端資料科學用戶端連接時, 您可以使用 RevoScaleR 函數, 在 SQL Server 的內容中執行 R 函數。 這和先前的工作流程不同，下圖會摘要說明。

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. 針對 RevoScaleR 函式, R 執行時間會呼叫連結函式, 而該函式會接著呼叫 BxlServer。
2. BxlServer 會隨 Microsoft R 提供，且與 R 執行階段在分開的處理序中執行。
3. BxlServer 會判斷連線目標並使用 ODBC 初始化連線，並在 R 資料來源物件中將認證做為連接字串的一部分來傳遞。
4. BxlServer 會開啟 SQL Server 實例的連接。
5. 針對 R 呼叫, 會叫用啟動列服務, 這會開啟適當的啟動程式 (RLauncher)。 之後，R 程式碼的處理方式就類似從 T-SQL 執行 R 程式碼的處理方式。
6. RLauncher 會呼叫安裝在 SQL Server 電腦上的 R 執行時間實例。
7. 結果會傳回 BxlServer。
8. SQL 衛星管理與 SQL Server 和清除相關工作物件的通訊。
9. SQL Server 會將結果傳回到用戶端。

## <a name="see-also"></a>另請參閱

+ [SQL Server 中的擴充性架構](extensibility-framework.md)
+ [SQL Server 中的 Python 和機器學習擴充功能](extension-python.md)