---
title: 轉換預存程式的 R 程式碼
description: 將 R 程式碼遷移至 SQL Server 預存程式, 以進行方案部署, 並對 SQL Server 上的關聯式資料進行資料存取。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a2bd6db3aaae2c07f6f46aecce3e7df913fc2a9e
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470242"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>轉換 R 程式碼以在 SQL Server (資料庫內) 實例中執行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文提供有關如何修改 R 程式碼以在 SQL Server 中工作的高階指引。 

當您將 R 程式碼從 R Studio 或另一個環境移至 SQL Server 時, 程式碼通常會在不進一步修改的情況下運作: 例如, 如果程式碼很簡單, 例如採用一些輸入的函式, 並傳回值。 您也可以更輕鬆地移植使用**RevoScaleR**或**MicrosoftML**套件的解決方案, 這可支援在不同的執行內容中以最少的變更來執行。

不過, 如果有下列任何一種情況, 您的程式碼可能會需要大量的變更:

+ 您可以使用存取網路或無法安裝在 SQL Server 上的 R 程式庫。
+ 此程式碼會對 SQL Server 以外的資料來源進行個別呼叫, 例如 Excel 工作表、共用上的檔案, 以及其他資料庫。 
+ 您想要在 *@script* [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的參數中執行程式碼, 也會參數化預存程式。
+ 您的原始解決方案包含多個步驟, 在生產環境中可能會更有效率 (如果獨立執行), 例如資料準備或特徵工程與模型定型、評分或報告。
+ 您想要藉由變更程式庫、使用平行執行, 或卸載部分處理 SQL Server, 來改善效能。 

## <a name="step-1-plan-requirements-and-resources"></a>步驟 1： 規劃需求和資源

**套件**

+ 判斷所需的套件, 並確保它們能在 SQL Server 上執行。
 
+ 在 Machine Learning 服務所使用的預設封裝程式庫中, 預先安裝套件。 不支援使用者程式庫。

**資料來源** 

+ 如果您想要將 R 程式碼內嵌在[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)中, 請識別主要和次要資料來源。 

    + **主要**資料來源是大型資料集, 例如模型定型資料, 或用於預測的輸入資料。 規劃將最大的資料集對應至[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的輸入參數。

    + **次要**資料來源通常是較小的資料集, 例如因素清單或其他群組變數。 
    
    目前, sp_execute_external_script 僅支援使用單一資料集做為預存程式的輸入。 不過, 您可以新增多個純量或二進位輸入。

    前面加上 EXECUTE 的預存程序呼叫, 無法當做[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的輸入使用。 您可以使用查詢、views 或任何其他有效的 SELECT 語句。

+ 判斷您需要的輸出。 如果您使用 sp_execute_external_script 執行 R 程式碼, 則預存程式只會輸出一個資料框架做為結果。 不過, 您也可以輸出多個純量輸出, 包括以二進位格式繪製和模型, 以及衍生自 R 程式碼或 SQL 參數的其他純量值。

**資料類型**

+ 建立可能資料類型問題的檢查清單。

    所有 R 資料類型都受到 SQL Server 機器學習服務的支援。 不過, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援的資料類型比 R 更多。因此, 在將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料傳送至 R 時, 會執行某些隱含資料類型轉換, 反之亦然。 您可能需要明確地轉換或轉換某些資料。 

    支援 NULL 值。 不過, R 會使用`na`資料結構來表示遺漏值, 這類似于 null。

+ 請考慮消除 R 無法使用的資料相依性: 例如, 來自 SQL Server 的 rowid 和 GUID 資料類型無法由 R 取用, 並產生錯誤。

    如需詳細資訊, 請參閱[R 程式庫和資料類型](../r/r-libraries-and-data-types.md)。

## <a name="step-2-convert-or-repackage-code"></a>步驟 2： 轉換或重新封裝程式碼

您變更程式碼的程度取決於您是否想要從遠端用戶端提交 R 程式碼, 以便在 SQL Server 計算內容中執行, 或想要在預存程式中部署程式碼, 這樣可以提供更好的效能和資料安全性。 將程式碼包裝在預存程式中會強加一些額外的需求。 

+ 盡可能將您的主要輸入資料定義為 SQL 查詢, 以避免資料移動。

+ 在預存程式中執行 R 時, 您可以傳遞多個純量輸入。 針對您想要在輸出中使用的任何參數, 加入**output**關鍵字。 

    例如, 下列純量輸入`@model_name`包含模型名稱, 這也會在結果的本身資料行中輸出:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 您傳入做為預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)之參數的任何變數, 都必須對應至 R 程式碼中的變數。 變數預設會依名稱對應。

    輸入資料集中的所有資料行也必須對應至 R 腳本中的變數。  例如, 假設您的 R 腳本包含如下的公式:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    如果輸入資料集未包含具有相符名稱 ArrDelay、CRSDepTime、DayOfWeek、Crsdephour 這些和 DayOfWeek 的資料行, 就會引發錯誤。

+ 在某些情況下, 必須事先定義結果的輸出架構。

    例如, 若要將資料插入資料表中, 您必須使用**WITH RESULT SET**子句來指定架構。

    如果 R 腳本使用引數`@parallel=1`, 則也需要輸出架構。 這是因為 SQL Server 可能建立多個處理序來平行執行查詢，並在最後收集結果。 因此, 您必須先備妥輸出架構, 才能建立平行處理常式。
    
    在其他情況下, 您可以使用選項搭配 [**未定義結果集**] 來省略結果架構。 這個語句會從 R 腳本傳回資料集, 而不需要命名資料行或指定 SQL 資料類型。

+ 請考慮使用 T-sql 而非 R 來產生計時或追蹤資料。

    例如, 您可以藉由新增傳遞至結果的 T-sql 呼叫, 而不是在 R 腳本中產生類似的資料, 來傳遞用於審核和儲存的系統時間或其他資訊。 

**改善效能和安全性**

+ 避免將預測或中繼結果寫入檔案。 改為將預測寫入資料表, 以避免資料移動。

+ 事先執行所有查詢, 並檢查 SQL Server 查詢計劃, 以識別可平行執行的工作。

    如果可以平行處理輸入查詢, 請將`@parallel=1`設定為[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)引數的一部分。 

    只要 SQL Server 可以與資料分割資料表搭配運作，或在多個處理序之間分散查詢並在最後彙總結果，通常就可以使用此旗標來進行平行處理。 如果您使用要求讀取所有資料的演算法來訓練模型，或是您需要建立彙總，則通常無法使用此旗標來進行平行處理。

+ 檢閱您的 R 程式碼，以判斷是否有步驟可藉由使用個別的預存程序呼叫，來獨立執行或以更有效率的方式執行。 例如, 您可以單獨執行特徵工程或功能解壓縮, 並將值儲存至資料表, 以獲得較佳的效能。

+ 針對以集合為基礎的計算, 尋找使用 T-sql 而非 R 程式碼的方式。

    例如, 此 R 解決方案會顯示使用者定義的 T-sql 函式和 R 如何執行相同的功能工程工作:[資料科學端對端](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)逐步解說。

+ 可能的話, 請將傳統 R 函數取代為支援分散式執行的**ScaleR**函數。 如需詳細資訊, 請參閱[基底 R 和調整 R 函數的比較](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)。

+ 請洽詢資料庫開發人員, 藉由使用 SQL Server 的功能 (例如[記憶體優化資料表](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)), 或如果您有 Enterprise Edition, [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)) 來判斷改善效能的方式。

    如需詳細資訊, 請參閱[分析服務的 SQL Server 優化秘訣和訣竅](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>步驟 3： 準備部署

+ 通知系統管理員，以便在部署程式碼之前，先安裝和測試套件。 

    在開發環境中, 您可以將套件安裝為程式碼的一部分, 但這在生產環境中是不好的作法。 

    無論您使用的是預存程式, 還是在 SQL Server 計算內容中執行 R 程式碼, 都不支援使用者程式庫。

**在預存程式中封裝您的 R 程式碼**

+ 如果您的程式碼相當簡單, 您可以在不需修改的情況下, 將它內嵌在 T-sql 使用者定義函數中, 如下列範例所述:

    + [建立在 rxExec 中執行的 R 函式](../tutorials/deepdive-create-a-simple-simulation.md)
    + [使用 T-sql 和 R 的特徵工程設計](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ 如果程式碼更複雜, 請使用 R 封裝**sqlrutils**來轉換您的程式碼。 此套件的設計目的是要協助有經驗的 R 使用者撰寫良好的預存程式程式碼。 

    第一個步驟是使用明確定義的輸入和輸出, 將您的 R 程式碼重寫為單一函式。

    然後, 使用**sqlrutils**套件, 以正確的格式產生輸入和輸出。 **Sqlrutils**封裝會為您產生完整的預存程式程式碼, 而且也可以在資料庫中註冊預存程式。 

    如需詳細資訊和範例, 請參閱[sqlrutils (SQL)](ref-r-sqlrutils.md)。

**與其他工作流程整合**

+ 利用 T-sql 工具和 ETL 程式。 在資料工作流程中預先執行功能工程設計、功能解壓縮和資料清理。

    當您在專用的 R 開發環境 (例如[!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)]或 RStudio) 中工作時, 可能會將資料提取到您的電腦、反復分析資料, 然後寫出或顯示結果。 
    
    不過, 將獨立 R 程式碼遷移至 SQL Server 時, 就可以簡化此程式, 或將其委派給其他 SQL Server 工具。 

+ 使用安全、非同步視覺化策略。

    SQL Server 的使用者通常無法存取伺服器上的檔案, 而且 SQL 用戶端工具通常不支援 R 圖形裝置。 如果您在方案中產生繪圖或其他圖形, 請考慮將繪圖匯出為二進位資料, 並儲存至資料表或寫入。

+ 將預測和計分函數包裝在預存程式中, 以供應用程式直接存取。

### <a name="other-resources"></a>其他資源

若要查看如何在 SQL Server 中部署 R 解決方案的範例, 請參閱下列範例:

+ [使用 R 和 SQL Server 建立 ski 出租企業的預測性模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [適用于 SQL 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)示範如何將 R 程式碼包裝在預存程式中, 使其更具模組化

+ [端對端資料科學解決方案](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)包含 R 和 T-sql 中的功能工程比較
