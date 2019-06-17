---
title: 轉換 R 程式碼，預存程序-SQL Server Machine Learning 服務
description: 將 R 程式碼移轉至 SQL Server 上的關聯式資料的解決方案部署和資料存取的 SQL Server 預存程序。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a3348058b03ff1441256cc8298ddc1b5b2216b0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642771"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>轉換 R 程式碼，以便在 SQL Server （資料庫內） 執行個體中執行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章提供如何修改 R 程式碼，才能在 SQL Server 中的高階指引。 

當您將 R 程式碼從 R Studio 或另一個環境移至 SQL Server 時，通常程式碼的運作不需要進一步修改： 例如，如果程式碼很簡單，例如接受部分的函式輸入，並傳回值。 它也很容易使用的連接埠解決方案**RevoScaleR**或是**MicrosoftML**支援幾乎不需要變更的不同執行內容中執行的封裝。

不過，您的程式碼可能需要大幅變更，如果有的話則適用下列步驟：

+ 您使用 R 程式庫，存取網路或無法在 SQL Server 上安裝的。
+ 程式碼會個別呼叫 SQL Server 外部的資料來源，例如 Excel 工作表、 共用上的檔案和其他資料庫。 
+ 您想要執行程式碼 *@script* 參數[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)並也參數化預存程序。
+ 與原始方案包含多個步驟，可能會在生產環境中執行資料準備或特徵工程設計與模型定型、 評分或報告等的各自獨立地如果更有效率。
+ 您想要改善效能發揮到程式庫，是使用平行執行，或變更某些將處理卸載至 SQL Server。 

## <a name="step-1-plan-requirements-and-resources"></a>步驟 1： 計劃需求與資源

**套件**

+ 判斷需要哪些封裝，並確保它們在 SQL Server 上運作。
 
+ 在 Machine Learning 服務所使用的預設套件程式庫中預先安裝套件。 不支援使用者程式庫。

**資料來源** 

+ 如果您想要將 R 程式碼中的內嵌[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，識別主要和次要資料來源。 

    + **主要**資料來源是大型資料集，例如模型訓練資料或用於預測的輸入的資料。 將您最大的資料集對應至輸入參數的計劃[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + **次要**資料來源是通常較小的資料集，例如的因素或其他群組變數的清單。 
    
    目前，sp_execute_external_script 支援單一資料集做為預存程序的輸入。 不過，您可以新增多個純量或二進位的輸入。

    預存程序呼叫如果前面有 EXECUTE 不能做為輸入來[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 您可以使用查詢、 檢視或任何其他有效 SELECT 陳述式。

+ 判斷您需要的輸出。 如果您執行使用 sp_execute_external_script 的 R 程式碼時，預存程序可以因此輸出只是一個資料框架。 不過，您也可以輸出多個純量的輸出，包括繪圖，而且衍生自 R 程式碼或 SQL 參數的二進位格式，以及其他純量值中的模型。

**資料類型**

+ 建立可能資料類型問題的檢查清單。

    SQL Server machine Learning 服務支援所有 R 資料類型。 不過，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援更多種類的資料類型比。傳送時，因此，執行某些隱含資料類型轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料至 R 時，反之亦然。 您可能需要明確轉型或轉換部分資料。 

    支援 NULL 值。 不過，會使用 R`na`資料建構來代表遺漏的值，類似於 null。

+ 請考慮消除相依性無法使用，例如 rowid r 的資料，並從 SQL Server 的 GUID 資料類型不能使用的 R，並產生錯誤。

    如需詳細資訊，請參閱 < [R 程式庫和資料型別](../r/r-libraries-and-data-types.md)。

## <a name="step-2-convert-or-repackage-code"></a>步驟 2： 轉換或重新封裝程式碼

變更您的程式碼的程度取決於您想要提交從遠端用戶端在 SQL Server 計算內容中執行的 R 程式碼，或想要部署的程式碼做為預存程序，可以提供較佳的效能和資料安全性的一部分。 您的程式碼包裝在預存程序會施加一些額外的需求。 

+ 可能的情況下，若要避免資料移動，請定義您主要的輸入的資料做為 SQL 查詢。

+ 當在預存程序中執行 R，您可以通過多個**純量**輸入。 針對任何您想要在輸出中所使用的參數，新增**輸出**關鍵字。 

    例如，下列的純量輸入`@model_name`包含模型名稱，這也是在自己的資料行在結果中的輸出：

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 您將傳遞做為參數的預存程序中的任何變數[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)必須對應至 R 程式碼中的變數。 變數預設會依名稱對應。

    輸入資料集中的所有資料行也必須對應至 R 指令碼中的變數。  例如，假設您的 R 指令碼包含此類公式：

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    如果輸入資料集不包含與 ArrDelay、 CRSDepTime、 DayOfWeek、 CRSDepHour 及 DayOfWeek 相符名稱的資料行，則會引發錯誤。

+ 在某些情況下，輸出結構描述必須事先為定義結果。

    例如，若要將資料插入資料表中，您必須使用**結果集與**子句來指定結構描述。

    如果 R 指令碼使用引數，都需要輸出結構描述`@parallel=1`。 這是因為 SQL Server 可能建立多個處理序來平行執行查詢，並在最後收集結果。 因此，在建立平行處理序之前，必須準備輸出結構描述。
    
    在其他情況下，您可以使用此選項省略結果結構描述**WITH RESULT SETS UNDEFINED**。 這個陳述式會傳回從 R 指令碼的資料集，而不需要命名資料行，或指定的 SQL 資料類型。

+ 請考慮產生使用 T-SQL，而不是 r 的時間設定或追蹤資料

    例如，您可以傳遞的系統時間或其他用於稽核和儲存體將會傳遞至結果的 T-SQL 呼叫，而不是在 R 指令碼中產生類似的資料的資訊。 

**改善效能和安全性**

+ 避免撰寫預測或檔案的中繼結果。 寫入預測資料表相反地，若要避免資料移動。

+ 事先執行所有的查詢，並檢閱 SQL Server 查詢計劃，識別可以以平行方式執行的工作。

    如果輸入的查詢可以平行處理，設定`@parallel=1`做為您的引數的一部分[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 

    只要 SQL Server 可以與資料分割資料表搭配運作，或在多個處理序之間分散查詢並在最後彙總結果，通常就可以使用此旗標來進行平行處理。 如果您使用要求讀取所有資料的演算法來訓練模型，或是您需要建立彙總，則通常無法使用此旗標來進行平行處理。

+ 檢閱您的 R 程式碼，以判斷是否有步驟可藉由使用個別的預存程序呼叫，來獨立執行或以更有效率的方式執行。 例如，您可能會收到較佳的效能，分別執行特性工程設計或功能擷取，並將值儲存至資料表。

+ 尋找使用 T-SQL，而不是 R 程式碼的集合為基礎的計算方式。

    例如，此 R 解決方案顯示方式的使用者定義的 T-SQL 函式，以及 R 可以執行相同的功能工程工作：[資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)。

+ 可能的話，取代傳統 R 函數**ScaleR**支援分散式的執行的函式。 如需詳細資訊，請參閱 <<c0> [ 比較的基底 R 和調整 R 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)。

+ 資料庫開發人員，以判斷如何使用 SQL Server 功能，例如改善效能，請洽詢[記憶體最佳化資料表](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)，或者，如果您有 Enterprise Edition [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor))。

    如需詳細資訊，請參閱[SQL Server 最佳化祕訣和訣竅分析服務](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>步驟 3： 準備部署

+ 通知系統管理員，以便在部署程式碼之前，先安裝和測試套件。 

    在開發環境中，可能可以將套件安裝為您的程式碼的一部分，但這是適合在生產環境中。 

    不支援使用者程式庫，不論您是使用預存程序或 SQL Server 計算內容中執行 R 程式碼。

**預存程序將 R 程式碼封裝**

+ 如果您的程式碼相當簡單，您可以將它內嵌在 T-SQL 使用者定義函式不需修改這些範例中所述：

    + [建立會在 rxExec 中執行的 R 函式](../tutorials/deepdive-create-a-simple-simulation.md)
    + [使用 T-SQL 和 R 的特徵工程設計](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ 如果程式碼更複雜，請使用 R 封裝**sqlrutils**轉換您的程式碼。 此套件可協助有經驗的 R 使用者撰寫良好的預存程序的程式碼。 

    第一個步驟是重寫為具有清楚定義的輸入和輸出的單一函式的 R 程式碼。

    然後，使用**sqlrutils**封裝來產生格式正確的輸入和輸出。 **Sqlrutils**封裝，產生完整的預存程序程式碼，也可以在資料庫中註冊預存程序。 

    如需詳細資訊和範例，請參閱 < [sqlrutils (SQL)](ref-r-sqlrutils.md)。

**與其他工作流程整合**

+ 利用 T-SQL 的工具和 ETL 程序。 執行特徵工程設計、 功能擷取和資料清理事先做為資料工作流程的一部分。

    當您使用專用的 R 開發環境中這類[!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)]或 RStudio，您可能會提取至您電腦的資料、 分析資料，然後寫出或顯示結果。 
    
    不過，當獨立 R 程式碼移轉至 SQL Server，此程序的大部分可以簡化或委派給其他 SQL Server 工具。 

+ 使用安全、 非同步的視覺效果的策略。

    SQL Server 使用者通常無法存取在伺服器上的檔案和 SQL 用戶端工具通常不支援 R 圖形裝置。 如果您產生繪圖或其他圖形做為方案的一部分時，請考慮將繪圖匯出為二進位資料並儲存至資料表，或寫入。

+ 應用程式所將預測和計分的函式包裝在預存程序進行直接存取。

### <a name="other-resources"></a>其他資源

若要檢視的方式部署 R 解決方案，在 SQL Server 中的範例，請參閱這些範例：

+ [建置使用 R 和 SQL Server 的 ski 租賃業務的預測性模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [SQL 開發人員的資料庫內分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)示範如何讓您的 R 程式碼更模組化藉由包裝預存程序

+ [端對端資料科學解決方案](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)包含 R 和 T-SQL 中的特徵工程設計的比較
