---
title: SQL Server 中的 R 延伸模組 |Microsoft Docs
description: 了解執行 R 程式碼和 SQL Server 中的內建 R 程式庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: af71b03238a744702288f1f7411a5ebec3911f60
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892864"
---
# <a name="r-extension-in-sql-server"></a>SQL Server 中的 R 延伸模組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R 延伸模組是以關聯式資料庫引擎的 SQL Server Machine Learning 服務附加元件的一部分。 它會新增 R 執行環境、 使用標準程式庫和工具的基底 R 散發和 Microsoft R 程式庫： [RevoScaleR](../r/revoscaler-overview.md)大規模的分析[MicrosoftML](../using-the-microsoftml-package.md)適用於 machine learning演算法和其他程式庫，以存取資料或 SQL Server 中的 R 程式碼。

從 SQL Server 2016 中的 SQL Server 中的 R 整合可[R Services](../r/sql-server-r-services.md)，並繼續向前一部分[SQL Server Machine Learning 服務](../what-is-sql-server-machine-learning.md)。

## <a name="r-components"></a>R 元件

SQL Server 包含開放原始碼和專屬套件。 透過 Microsoft 發佈的開放原始碼: Microsoft R 開啟 (MRO)，基底 R 程式庫進行安裝。 目前的 R 使用者應該能夠連接埠其 R 程式碼，並以幾乎不需要修改 SQL Server 上的外部處理序方式執行它。 MRO 安裝獨立於 SQL 工具和外部核心引擎的程序，在擴充性架構中執行。 在安裝期間，您必須同意的開放原始碼授權條款。 之後，您可以執行標準的 R 封裝，不需要進一步修改就如同在 r 的任何其他開放原始碼散發 

SQL Server 不會修改基底的 R 可執行檔，但您必須使用安裝程式安裝，因為該版本是專屬的套件，建置及測試上的 R 版本。 如需有關如何 MRO 不同，您可能會收到從 CRAN R 基底散發的詳細資訊，請參閱[R 語言和 Microsoft R 產品與功能的互通性](https://docs.microsoft.com/r-server/what-is-r-server-interoperability)。

安裝程式安裝 R 基底封裝散發可以位於執行個體相關聯的資料夾。 比方說，如果您在 SQL Server 2016 的預設執行個體上安裝 R Services，R 程式庫位於此資料夾預設： `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`。 同樣地，預設執行個體相關聯的 R 工具會位於此資料夾預設： `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`。

R 套件的平行和分散式工作負載，Microsoft 將加入包含下列的程式庫。

| 程式庫 | 描述 |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 支援資料來源物件和資料探索、 操作、 轉換和視覺效果。 它支援建立遠端計算內容，以及各種不同的可調整機器學習服務模型，例如**rxLinMod**。 API 已經最佳化，可分析因過大而無法納入記憶體的資料集，以及執行分散在數個核心或處理器上的計算。 RevoScaleR 封裝也支援 XDF 檔案格式更快速移動和儲存用於分析的資料。 XDF 格式會使用單欄式儲存體、具可攜性，且可用來從各種來源載入然後操作資料，包括文字、SPSS 或 ODBC 連線。 |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | 包含已針對速度及準確性，最佳化，以及內嵌轉換處理文字與映像的機器學習演算法。 如需詳細資訊，請參閱 <<c0> [ 使用 MicrosoftML 封裝與 SQL Server](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package)。 | 

## <a name="using-r-in-sql-server"></a>在 SQL Server 中使用 R

您可以編寫指令碼 R 中使用基底的函式，但可受益於多重處理，您必須匯入**RevoScaleR**並**MicrosoftML**模組到您的 R 程式碼和其函式來建立模型，然後呼叫以平行方式執行。 
 
支援的資料來源包含 ODBC 資料庫、 SQL Server 與 XDF 檔案格式交換資料與其他來源，或使用 R 解決方案。 輸入的資料必須是表格式。 所有的 R 結果必須為資料框架的形式傳回。

支援的計算內容包括本機或遠端 SQL Server 計算內容。 在遠端計算內容是指在工作站上，例如一部電腦啟動的程式碼執行，但參數然後指令碼到遠端電腦的執行。 切換計算內容時，需要兩個系統都有相同的 RevoScaleR 程式庫。

本機計算內容，如您所料，包括執行資料庫引擎執行個體，與相同的伺服器上使用 T-SQL 程式碼的 R 程式碼，或內嵌在預存程序。 您也可以從本機的 R IDE 中執行程式碼，並可在 SQL Server 電腦上執行，藉由定義遠端計算內容的指令碼。

## <a name="execution-architecture"></a>執行架構

下列圖表說明 SQL Server 元件的互動與 R 執行階段中每個支援的案例： 從 R 命令列，使用 SQL Server 計算內容中執行指令碼在資料庫和遠端執行。

### <a name="r-scripts-executed-from-sql-server-in-database"></a>從 SQL Server 資料庫內執行的 R 指令碼

從 SQL Server 會藉由呼叫預存程序執行 「 內部 」 執行的 R 程式碼。 因此，任何可以進行預存程序呼叫的應用程式都能初始化 R 程式碼的執行。  之後 SQL Server 管理 R 程式碼在下圖摘要說明的執行。

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. 對於 R 執行階段的要求會以傳遞到預存程序 ([sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)) 的參數 _@language='R'_ 表示。 SQL Server 會將此要求傳送到 Launchpad 服務。
2. Launchpad 服務會啟動適當的啟動器，在此案例中為 RLauncher。
3. RLauncher 啟動外部 R 處理序。
4. BxlServer 會與 R 執行階段管理的 SQL server 的資料交換及處理結果的儲存協調。
5. SQL Satellite 管理相關的工作和程序與 SQL Server 的通訊。
6. BxlServer 使用 SQL Satellite 來傳達狀態，以及 SQL Server 的結果。
7. SQL Server 取得結果，並關閉相關的工作和程序。

### <a name="r-scripts-executed-from-a-remote-client"></a>從遠端用戶端執行的 R 指令碼

從支援 Microsoft R 的遠端資料科學用戶端連線時，您可以在 SQL Server 的內容中執行 R 函數，使用 RevoScaleR 函式項目。 這和先前的工作流程不同，下圖會摘要說明。

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. 對於 RevoScaleR 函式，R 執行階段會呼叫連結的函式再進而呼叫 BxlServer。
2. BxlServer 會隨 Microsoft R 提供，且與 R 執行階段在分開的處理序中執行。
3. BxlServer 會判斷連線目標並使用 ODBC 初始化連線，並在 R 資料來源物件中將認證做為連接字串的一部分來傳遞。
4. BxlServer 開啟 SQL Server 執行個體的連接。
5. 針對 R 呼叫，Launchpad 會叫用服務，進而啟動適當的啟動器 RLauncher。 之後，R 程式碼的處理方式就類似從 T-SQL 執行 R 程式碼的處理方式。
6. Rlauncher 呼叫 SQL Server 電腦上已安裝的 R 執行階段的執行個體。
7. 結果會傳回 BxlServer。
8. SQL Satellite 管理與 SQL Server 與清除作業相關的工作物件的通訊。
9. SQL Server 會將結果傳遞回用戶端。

## <a name="see-also"></a>另請參閱

+ [SQL Server 中的擴充性架構](extensibility-framework.md)
+ [Python 和機器學習服務在 SQL Server 中的延伸模組](extension-python.md)