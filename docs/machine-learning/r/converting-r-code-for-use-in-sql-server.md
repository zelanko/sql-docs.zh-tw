---
title: 轉換 R 程式碼以用於 SQL
description: 將 R 程式碼移轉到 SQL Server 預存程序，以進行方案部署，以及對 SQL Server 上的關聯式資料進行資料存取。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/28/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 009ce927481a455478e170cbe075e920d72571f3
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288298"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>轉換 R 程式碼以在 SQL Server (資料庫內) 執行個體中執行
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

本文提供有關如何修改 R 程式碼以在 SQL Server 中運作的高階指引。 

當您將 R 程式碼從 R Studio 或另一個環境移至 SQL Server 時，程式碼大都可在不進一步修改的情況下運作：例如，程式碼很簡單，像是接受一些輸入並傳回值的函式。 您也可以更輕鬆地移植使用 **RevoScaleR** 或 **MicrosoftML** 套件的解決方案，以支援在進行最少量變更的情況下，於不同的執行內容中執行。

不過，如果發生下列任何一種情況，您的程式碼可能會需要大量變更：

+ 您可以使用存取網路或無法在 SQL Server 上安裝的 R 程式庫。
+ 此程式碼會對 SQL Server 外部的資料來源 (例如 Excel 工作表、共用上的檔案，以及其他資料庫) 進行個別呼叫。 
+ 您想要在 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的 *\@script* 參數中執行程式碼，同時也希望將預存程序參數化。
+ 您的原始解決方案包含在生產環境中獨立執行時可能會更有效率的多個步驟，例如資料準備或特徵工程與模型定型、評分或報告。
+ 您想要藉由變更程式庫、使用平行執行，或將部分處理作業卸載至 SQL Server，希望能藉此改善效能。 

## <a name="step-1-plan-requirements-and-resources"></a>步驟 1： 計劃資源和需求

**套件**

+ 決定需要哪些套件，並確保它們可在 SQL Server 上運作。
 
+ 請在機器學習服務使用的預設封裝程式庫中預先安裝套件。 不支援子程式庫。

**資料來源** 

+ 如果您想要在 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中內嵌 R 程式碼，請識別主要和次要資料來源。 

    + **主要** 資料來源是大型資料集 (例如模型定型資料)，或用於預測的輸入資料。 請計劃將您最大的資料集對應到 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的輸入參數。

    + **次要** 資料來源通常是較小的資料集，例如因素清單或其他群組變數。 
    
    目前，sp_execute_external_script 僅支援使用單一資料集做為預存程序的輸入。 但是，您可以新增多個純量或二進位輸入。

    預存程序呼叫如果前面有 EXECUTE，就無法用來作為 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的輸入。 您可以使用查詢、檢視或任何其他有效的 SELECT 陳述式。

+ 判斷您需要的輸出。 如果您使用 sp_execute_external_script 執行 R 程式碼，則預存程序只會輸出一個資料框架做為結果。 但是，您也可以輸出多個純量輸出，包括二進位格式的繪圖與模型，以及衍生自 R 程式碼或 SQL 參數的其他純量值。

**資料類型**

+ 建立可能資料類型問題的檢查清單。

    SQL Server 機器學習服務支援所有 R 資料類型。 不過，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援的資料類型比 R 更多樣。因此將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料傳送給 R (和反向傳送) 時，會執行一些隱含的資料類型轉換。 您可能需要明確地將某些資料轉型或轉換。 

    支援 NULL 值。 但是，R 使用 `na` 資料建構來代表遺漏值，這類似於 Null。

+ 請考慮消除 R 所無法使用資料的相依性：例如，R 無法使用來自 SQL Server 的 rowid 和 GUID 資料類型並且會產生錯誤。

    如需詳細資訊，請參閱 [R 程式庫和資料類型](../r/r-libraries-and-data-types.md)。

## <a name="step-2-convert-or-repackage-code"></a>步驟 2： 轉換或重新封裝程式碼

程式碼的變更程度取決於您是否想要從遠端用戶端提交 R 程式碼，以便在 SQL Server 計算內容中執行，或嘗試在預存程序中部署程式碼，這可以提供更好的效能和資料安全性。 將程式碼包裝在預存程序中會增加一些額外需求。 

+ 請盡可能將您的主要輸入資料定義為 SQL 查詢，以避免資料移動。

+ 在預存程序中執行 R 時，您可以傳遞多個**純量**輸入。 針對您想要在輸出中使用的任何參數，請加入 **OUTPUT** 關鍵字。 

    例如，下列純量輸入 `@model_name` 包含模型名稱，這也會在結果中它自己的資料行中輸出：

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 您以 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 預存程序參數形式傳送的任何變數，都必須與 R 程式碼中的變數對應。 變數預設會依名稱對應。

    輸入資料集內的所有資料行也都必須與 R 指令碼中的變數對應。  例如，假設您的 R 指令碼包含如以下的公式：

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    如果輸入資料集並未包含與 ArrDelay、CRSDepTime、DayOfWeek、CRSDepHour 及 DayOfWeek 名稱相符的資料行，就會引發錯誤。

+ 在某些情況下，必須事先定義結果的輸出架構。

    例如，若要將資料插入資料表中，您必須使用 **WITH RESULT SET** 子句來指定架構。

    如果您的 R 指令碼使用引數 `@parallel=1`，就必須提供輸出結構描述。 這是因為 SQL Server 可能建立多個處理序來平行執行查詢，並在最後收集結果。 因此，必須先準備好輸出結構描述，才能建立平行處理序。
    
    在其他情況下，您可以使用 **WITH RESULT SETS UNDEFINED** 選項來省略結果架構。 此陳述式會從 R 指令碼傳回資料集，而不需要將資料行命名或指定 SQL 資料類型。

+ 請考慮使用 T-SQL (而非 R) 來產生計時或追蹤資料。

    例如，您可以藉由新增傳遞至結果的 T-SQL 呼叫 (而不是在 R 指令碼中產生類似的資料)，來傳遞用於審核和儲存的系統時間或其他資訊。 

**改善效能和安全性**

+ 避免將預測或中繼結果存檔。 改為將預測寫入資料表，以避免資料移動。

+ 先執行所有查詢，然後檢閱 SQL Server 查詢計劃來識別可平行執行的工作。

    如果可以平行處理輸入查詢，請設定 `@parallel=1` 作為您 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 引數的一部分。 

    只要 SQL Server 可以與資料分割資料表搭配運作，或在多個處理序之間分散查詢並在最後彙總結果，通常就可以使用此旗標來進行平行處理。 如果您使用要求讀取所有資料的演算法來訓練模型，或是您需要建立彙總，則通常無法使用此旗標來進行平行處理。

+ 檢閱您的 R 程式碼，以判斷是否有步驟可藉由使用個別的預存程序呼叫，來獨立執行或以更有效率的方式執行。 例如，您可以透過將特徵工程或特徵擷取分開執行，並將值儲存至資料表，來獲得更好的效能。

+ 尋找使用 T-SQL 而不使用 R 程式碼來進行集合型計算的方式。

    例如，這個 R 解決方案會顯示使用者定義的 T-SQL 函式和 R 如何執行相同的特徵工程工作：[資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)。

+ 如有可能，請以支援分散式執行的 **ScaleR** 函數取代傳統 R 函數。 如需詳細資訊，請參閱 [Base R 與 Scale R 函數的比較](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)。

+ 請洽詢資料庫開發人員，以判斷藉由使用像是[經記憶體最佳化的資料表](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)這樣的 SQL Server 功能，或者，如果您有 Enterprise Edition，則使用 [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)來改善效能的方式。


### <a name="step-3-prepare-for-deployment"></a>步驟 3： 準備開始部署

+ 通知系統管理員，以便在部署程式碼之前，先安裝和測試套件。 

    在開發環境中，在安裝您的程式碼時一併安裝套件或許是可行的方式，但在生產環境中則是一個不好的做法。 

    無論您使用的是預存程序，或是在 SQL Server 計算內容中執行 R 程式碼，都不支援使用者程式庫。

**在預存程序中封裝 R 程式碼**

+ 如果您的程式碼較簡單，則可以在不修改的情況下，將其內嵌在 T-SQL 使用者定義函式中，如此範例中所述：

    + [ 使用 T-SQL 和 R 的特徵工程](../tutorials/r-taxi-classification-create-features.md)

+ 如果程式碼比較複雜，請使用 R 封裝 **sqlrutils** 來轉換您的程式碼。 此套件的設計目的是要協助有經驗的 R 使用者撰寫良好的預存程序程式碼。 

    第一個步驟是使用明確定義的輸入和輸出，將您的 R 程式碼重寫為單一函式。

    然後，使用 **sqlrutils** 套件來以正確的格式產生輸入和輸出。 **sqlrutils** 封裝會為您產生完整的預存程序程式碼，而且也可以在資料庫中註冊預存程序。 

    如需詳細資訊和範例，請參閱 [sqlrutils (SQL)](ref-r-sqlrutils.md)。

**與其他工作流程整合**

+ 利用 T-SQL 工具和 ETL 程序。 在資料工作流程中預先執行特徵工程、特徵擷取，以及資料清理。

    當您在像是 [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] 或 RStudio 這樣的專用 R 開發環境中工作時，您可以將資料提取到您的電腦、反覆分析該資料，然後寫出或顯示結果。 
    
    不過，將獨立 R 程式碼移轉到 SQL Server 時，此程序大部分都可簡化或委派給其他 SQL Server 工具來執行。 

+ 使用安全、非同步視覺化策略。

    SQL Server 的使用者通常無法存取伺服器上的檔案，而且 SQL 用戶端工具通常不支援 R 圖形裝置。 如果您在解決方案中產生繪圖或其他圖形，請考慮將繪圖匯出為二進位資料，並儲存至資料表或寫入。

+ 將預測和評分函式包裝在預存程序中以供應用程式直接存取。

### <a name="other-resources"></a>其他資源

若要檢視如何在 SQL Server 中部署 R 解決方案的範例，請參閱下列範例：

+ [使用 R 和 SQL Server 建置滑雪租賃企業預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [SQL 開發人員適用的資料庫內分析](../tutorials/r-taxi-classification-introduction.md)示範了如何將 R 程式碼包裝在預存程序中來使它更加模組化

+ [端對端資料科學解決方案](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)包含 R 和 T-SQL 中特徵工程的比較
