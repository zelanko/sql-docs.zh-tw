---
title: R 語言延伸模組
description: 了解 SQL Server R 服務或 SQL Server 機器學習服務中的 R 程式碼執行以及內建 R 程式庫。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 98ef57702b01a3f32babd6b0ac9b64fb3c22e9ea
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727656"
---
# <a name="r-language-extension-in-sql-server"></a>SQL Server 中的 R 語言延伸模組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R 延伸模組是 SQL Server 機器學習服務對關聯式資料庫引擎的附加元件之一。 此延伸模組會新增 R 執行環境、基底 R 發行版本 (含標準程式庫和工具)，以及 Microsoft R 程式庫：適用於大規模分析的 [RevoScaleR](../r/ref-r-revoscaler.md)、適用於機器學習演算法的 [MicrosoftML](../r/ref-r-microsoftml.md)，以及用來在 SQL Server 中存取資料或 R 程式碼的其他程式庫。

[SQL Server R 服務](../r/sql-server-r-services.md)和 [SQL Server 機器學習服務](../what-is-sql-server-machine-learning.md)均提供 R 整合。

## <a name="r-components"></a>R 元件

SQL Server 包含開放原始碼和專屬套件。 系統會透過下列 Microsoft 開放原始碼 R 發行版本來安裝基底 R 程式庫：Microsoft R Open (MRO)。 目前的 R 使用者應該只需進行極少修改，即可移植其 R 程式碼，並在 SQL Server 上以外部處理序的形式執行。 MRO 是獨立安裝的 SQL 工具，並在擴充性架構中的核心引擎處理序外部執行。 在安裝期間，您必須同意開放原始碼授權條款。 之後，您就可以執行標準 R 套件，而不需進一步修改，如同您在 R 的任何其他開放原始碼發行版本中一樣。 

SQL Server 不會修改基底 R 可執行檔，但您必須使用安裝程式所安裝的 R 版本，因為該版本是專屬套件據以建立和測試的版本。 如需 MRO 與 R 基底發行版本 (透過 CRAN 取得) 之間的差異詳細資訊，請參閱 [Interoperability with R language and Microsoft R products and features](https://docs.microsoft.com/r-server/what-is-r-server-interoperability) (R 語言和 Microsoft R 產品及功能的互通性)。

您可以在與執行個體建立關聯的資料夾中，找到安裝程式安裝的 R 基底套件發行版本。 例如，如果您已在 SQL Server 預設執行個體上安裝 R 服務，則根據預設，R 程式庫會位於 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library` 資料夾中。 同樣地，根據預設，與預設執行個體建立關聯的 R 工具會位於 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 資料夾中。

Microsoft 為平行和分散式工作負載新增的 R 套件包含下列程式庫。

| 程式庫 | 描述 |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 支援資料來源物件和資料探索、操作、轉換和視覺化。 RevoScaleR 支援建立遠端計算內容，以及各種可調整的機器學習模型，例如 **rxLinMod**。 API 已經最佳化，可分析因過大而無法納入記憶體的資料集，以及執行分散在數個核心或處理器上的計算。 RevoScaleR 套件也支援 .XDF 檔案格式，以便更快速移動和儲存用於分析的資料。 XDF 格式會使用單欄式儲存體、具可攜性，且可用來從各種來源載入然後操作資料，包括文字、SPSS 或 ODBC 連線。 |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | 包含已針對速度和正確性最佳化的機器學習演算法，以及適用於處理文字和影像的內嵌轉換。 如需詳細資訊，請參閱 [SQL Server 中的 MicrosoftML](../r/ref-r-microsoftml.md)。 | 

## <a name="using-r-in-sql-server"></a>在 SQL Server 中使用 R

您可以使用基底函式編寫 R 指令碼，但若要獲得多重處理的優點，您必須將 **RevoScaleR** 和 **MicrosoftML** 模組匯入您的 R 程式碼，然後呼叫其函式來建立可平行執行的模型。 
 
系統支援 ODBC 資料庫、SQL Server 和 XDF 檔案格式等資料來源，以便與其他來源或 R 解決方案交換資料。 輸入資料必須為表格式。 所有 R 結果都必須以資料框架的形式傳回。

支援的計算內容包括本機或遠端 SQL Server 計算內容。 遠端計算內容是指在某一部電腦 (例如工作站) 上啟動的程式碼執行，但接著將指令碼執行切換至遠端電腦的情況。 若要切換計算內容，這兩個系統都需要具備相同的 RevoScaleR 程式庫。

如您所預期，本機計算內容會執行位於資料庫引擎執行個體所在相同伺服器上的 R 程式碼，以及 T-SQL 內部或內嵌於預存程式中的程式碼。 您也可以定義遠端計算內容，以從本機 R IDE 執行程式碼，並在 SQL Server 電腦上執行指令碼。

## <a name="execution-architecture"></a>執行架構

下圖說明在每個支援案例中，SQL Server 元件與 R 執行階段的互動情況：使用 SQL Server 計算內容，在資料庫中執行指令碼，以及從 R 命令列遠端執行。

### <a name="r-scripts-executed-from-sql-server-in-database"></a>從 SQL Server 資料庫內執行的 R 指令碼

系統會透過呼叫預存程序來執行從 SQL Server「內部」執行的 R 程式碼。 因此，任何可以進行預存程序呼叫的應用程式都能初始化 R 程式碼的執行。  之後，SQL Server 會依下圖中的摘要說明來管理 R 程式碼執行。

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. 對於 R 執行階段的要求會以傳遞到預存程序 ([sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)) 的參數 _@language='R'_ 表示。 SQL Server 會將此要求傳送到啟動控制板服務。
在 Linux 中，SQL 會使用**啟動控制板**服務來與每個使用者的不同啟動控制板程序通訊。 如需詳細資料，請參閱[擴充性架構圖表](extensibility-framework.md#architecture-diagram)。
2. 啟動控制板服務會啟動適當的啟動器；在此案例中為 RLauncher。
3. RLauncher 啟動外部 R 處理序。
4. BxlServer 會與 R 執行階段協調來管理 SQL Server 資料交換與工作結果的儲存。
5. SQL Satellite 會管理與 SQL Server 之間相關工作和處理序的通訊。
6. BxlServer 會使用 SQL Satellite 來與 SQL Server 進行狀態和結果的通訊。
7. SQL Server 會取得結果，並關閉相關工作和處理序。

### <a name="r-scripts-executed-from-a-remote-client"></a>從遠端用戶端執行的 R 指令碼

從支援 Microsoft R 的遠端資料科學用戶端連線時，您可以使用 RevoScaleR 函式在 SQL Server 的內容中執行 R 函式。 這和先前的工作流程不同，下圖會摘要說明。

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. 針對 RevoScaleR 函式，R 執行階段會呼叫連結函式，由該函式呼叫 BxlServer。
2. BxlServer 會隨 Microsoft R 提供，且與 R 執行階段在分開的處理序中執行。
3. BxlServer 會判斷連線目標並使用 ODBC 初始化連線，並在 R 資料來源物件中將認證做為連接字串的一部分來傳遞。
4. 由 BxlServer 開啟對 SQL Server 執行個體的連線。
5. 針對 R 呼叫，系統會叫用啟動控制板服務，由其啟動適當的啟動器 RLauncher。 之後，R 程式碼的處理方式就類似從 T-SQL 執行 R 程式碼的處理方式。
6. RLauncher 會呼叫安裝在 SQL Server 電腦上 R 執行階段的執行個體。
7. 結果會傳回 BxlServer。
8. 由 SQL Satellite 管理與 SQL Server 的通訊，並清理相關的工作物件。
9. SQL Server 將結果傳回至用戶端。

## <a name="see-also"></a>另請參閱

+ [SQL Server 中的擴充性架構](extensibility-framework.md)
+ [SQL Server 的 Python 和機器學習延伸模組](extension-python.md)