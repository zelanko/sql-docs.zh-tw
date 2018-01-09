---
title: "轉換 R 程式碼以在 R Services 中使用 | Microsoft Docs"
ms.date: 12/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 595bdb9cb16b02258d50d1f3d038ad988bbc4dd3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="converting-r-code-for-execution-in-database"></a>轉換執行資料庫內的 R 程式碼

本文章提供有關如何修改工作在 SQL Server 中的 R 程式碼的高階指引。 

當您將 R 程式碼從 R Studio 或另一個環境移至 SQL Server 時，通常將程式碼的運作方式不需要進一步修改： 例如，如果程式碼是簡單的例如接受部分的函式輸入，並傳回值。 它也很容易使用的連接埠解決方案**RevoScaleR**或**MicrosoftML**支援最少變更的不同的執行內容中執行的封裝。

不過，您的程式碼可能需要大量變更，如果有則適用下列步驟：

+ 您使用 R 程式庫，存取網路或無法在 SQL Server 上安裝的。
+ 程式碼會對 SQL Server 外部的資料來源，例如 Excel 工作表、 共用上的檔案和其他資料庫不同的呼叫。 
+ 您想要執行的程式碼 *@script* 參數[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)和也參數化預存程序。
+ 與原始方案包含多個可能會更有效率，如果執行獨立作業，例如資料準備或特徵設計模型定型、 計分或 reporting 與在生產環境中的步驟。
+ 您想要改善藉由變更文件庫，使用平行執行，或某些將處理卸載至 SQL Server 最佳化效能。 

## <a name="step-1-plan-requirements-and-resources"></a>步驟 1： 規劃需求和資源

**套件**

+ 判斷需要哪些封裝，並確定可在 SQL Server 上。
 
+ 機器學習服務所使用的預設套件文件庫中，預先安裝套件。 不支援使用者文件庫。

**資料來源** 

+ 如果您想要將內嵌 R 程式碼中的[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，識別主要和次要資料來源。 

    + **主要**資料來源是大型資料集，例如模型定型資料或用於預測的輸入的資料。 要對應的輸入參數的最大資料集[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + **次要**資料來源是通常較小的資料集，例如的因素或其他的群組變數的清單。 
    
    目前，sp_execute_external_script 支援單一資料集做為預存程序的輸入。 不過，您可以加入多個純量或二進位的輸入。

    加上執行的預存程序呼叫不能做為輸入[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 您可以使用查詢、 檢視或任何其他有效 SELECT 陳述式。

+ 決定您需要的輸出。 如果您執行使用 sp_execute_external_script 的 R 程式碼，預存程序可以因此輸出一個資料框架。 不過，您也可以輸出多個純量的輸出，包括繪圖，衍生自 R 程式碼或 SQL 參數的二進位格式，以及其他純量值中的模型。

**資料類型**

+ 建立可能資料類型問題的檢查清單。

    SQL Server 機器學習服務會支援所有 R 資料類型。 不過，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援更多種類的資料型別比。傳送時，因此，執行某些隱含資料類型轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料 R，反之亦然。 您可能需要明確轉型或轉換部分資料。 

    支援 NULL 值。 不過，會使用 R`na`來表示遺漏值，類似於 null 的資料建構。

+ 請考慮排除相依性，例如 rowid： 無法使用的資料，從 SQL Server 的 GUID 資料類型不能使用的 R，並產生錯誤。

    如需詳細資訊，請參閱[R 程式庫和資料型別](../r/r-libraries-and-data-types.md)。

## <a name="step-2-convert-or-repackage-code"></a>步驟 2： 轉換或重新封裝程式碼

您變更程式碼的程度，取決於您想要提交從執行 SQL Server 計算內容中，遠端用戶端的 R 程式碼，或想要部署的程式碼做為預存程序，可以提供較佳的效能與資料安全性的一部分。 您的程式碼包裝在預存程序中加入了一些其他需求。 

+ 定義您主要的輸入的資料做為 SQL 查詢，可能的情況下，若要避免資料移動。

+ 當在預存程序中執行 R，您可以傳遞透過多個**純量**輸入。 針對您想要在輸出中使用任何參數，新增**輸出**關鍵字。 

    例如，下列的純量輸入`@model_name`包含模型的名稱，這也是在自己的資料行在結果中輸出：

    ```SQL
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 您將傳遞做為參數的預存程序中的任何變數[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)必須對應到變數中的 R 程式碼。 變數預設會依名稱對應。

    輸入資料集中的所有資料行也必須對應至 R 指令碼中的變數。  例如，假設您的 R 指令碼包含公式與下列類似：

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    如果輸入資料集不包含具有相符名稱 ArrDelay、 CRSDepTime、 DayOfWeek、 CRSDepHour 和 DayOfWeek 資料行，會引發錯誤。

+ 在某些情況下，輸出結構描述必須事先為定義結果。

    例如，若要將資料插入資料表中，您必須使用**與結果集**子句來指定結構描述。

    輸出結構描述也是必要的 R 指令碼會使用引數如果`@parallel=1`。 這是因為 SQL Server 可能建立多個處理序來平行執行查詢，並在最後收集結果。 因此，才能建立平行處理，必須準備輸出結構描述。
    
    在其他情況下，您可以使用此選項省略結果結構描述**與 RESULT SETS UNDEFINED**。 這個陳述式從 R 指令碼傳回資料集，而不需命名資料行，或指定的 SQL 資料類型。

+ 請考慮產生時間或追蹤資料使用 T-SQL，而不是。

    例如，您可以通過系統時間或其他用來稽核及存放裝置新增的 T-SQL 呼叫會傳遞到結果，而不是在 R 指令碼中產生類似的資料的資訊。 

**改善效能和安全性**

+ 避免撰寫預測或檔案的中繼結果。 寫入預測資料表相反地，若要避免資料移動。

+ 事先執行所有查詢，並檢閱 SQL Server 查詢計劃，來識別可以平行執行的工作。

    如果輸入的查詢可以平行處理，設定`@parallel=1`做為您的引數的一部分[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 

    只要 SQL Server 可以與資料分割資料表搭配運作，或在多個處理序之間分散查詢並在最後彙總結果，通常就可以使用此旗標來進行平行處理。 如果您使用要求讀取所有資料的演算法來訓練模型，或是您需要建立彙總，則通常無法使用此旗標來進行平行處理。

+ 檢閱您的 R 程式碼，以判斷是否有步驟可藉由使用個別的預存程序呼叫，來獨立執行或以更有效率的方式執行。 例如，您可能會收到較佳的效能分別執行特徵設計或擷取特徵，然後將值儲存到資料表。

+ 尋找集合為基礎的計算是使用 T-SQL，而不是 R 程式碼的方式。

    例如，此 R 解決方案會說明使用者定義的 T-SQL 函式，而 R 可以執行相同的功能工程工作：[資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)。

+ 可能的話，請取代傳統的 R 函數與**ScaleR**支援分散式的執行的函式。 如需詳細資訊，請參閱[比較的基底 R 和小數位數的 R 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)。

+ 資料庫開發人員決定要使用 SQL Server 功能，例如改善效能的方式，請洽詢[記憶體最佳化資料表](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)，或者，如果您有企業版[資源管理員](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor))。

    如需詳細資訊，請參閱[SQL Server 最佳化的秘訣和訣竅分析服務](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>步驟 3： 準備部署

+ 通知系統管理員，以便在部署程式碼之前，先安裝和測試套件。 

    在開發環境中，可能還是可以做為您的程式碼的一部分安裝封裝，但這是不正確的作法是在生產環境中。 

    不支援使用者文件庫，不論您是使用預存程序或 SQL Server 計算內容中執行 R 程式碼。

**封裝的預存程序中的 R 程式碼**

+ 如果您的程式碼相當簡單，您可以將它內嵌在 T-SQL 使用者自訂函數不需修改這些範例中所述：

    + [建立會在 rxExec 中執行的 R 函數](..\tutorials\deepdive-create-a-simple-simulation.md)
    + [使用 T-SQL 和 R 功能工程](..\tutorials\sqldev-create-data-features-using-t-sql.md)

+ 如果程式碼更複雜，請使用 R 封裝**sqlrutils**轉換您的程式碼。 此封裝被為了幫助經驗豐富的 R 使用者撰寫好預存程序程式碼。 

    第一個步驟是將 R 程式碼改寫具有明確定義的輸入和輸出的單一函式。

    然後，使用**sqlrutils**產生格式正確的輸入和輸出的封裝。 **Sqlrutils**封裝產生完整的預存程序程式碼，和也在資料庫中註冊預存程序。 

    如需詳細資訊和範例，請參閱[SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)。

**與其他工作流程整合**

+ 利用 T-SQL 的工具和 ETL 程序。 執行特徵設計、 擷取特徵，以及資料清理事先做為資料工作流程的一部分。

    當您使用專用的 R 開發環境中這類[!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)]或 RStudio，您可能資料提取到您的電腦、 反覆，分析資料然後寫出或顯示結果。 
    
    不過，當您獨立 R 程式碼移轉至 SQL Server，此程序的許多簡化或委派給其他 SQL Server 工具。 

+ 使用安全且非同步的視覺效果的策略。

    SQL Server 的使用者通常無法存取伺服器上的檔案和 SQL 用戶端工具通常不支援 R 圖形裝置。 如果您產生繪圖或其他圖形做為方案的一部分，請考慮將圖匯出為二進位資料並儲存至資料表，或寫入。

+ 應用程式將預測和計分函式包裝在預存程序，針對直接存取。

### <a name="other-resources"></a>其他資源

若要檢視的方式部署 R 解決方案，SQL Server 中的範例，請參閱這些範例：

+ [建置 ski 以租用方式佔用商務使用 R 和 SQL Server 的預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [資料庫在分析 SQL 開發人員](../tutorials/sqldev-in-database-r-for-sql-developers.md)示範如何讓您的 R 程式碼更模組化其包裝在預存程序

+ [端對端資料科學方案](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)R 和 T-SQL 中包含的功能工程比較
