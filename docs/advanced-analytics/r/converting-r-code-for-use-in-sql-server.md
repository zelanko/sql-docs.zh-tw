---
title: "轉換 R 程式碼以在 R Services 中使用 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 06/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e861a139af2c4aad159920a6659a0598091439b8
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="converting-r-code-for-use-in-r-services"></a>轉換 R 程式碼以在 R Services 中使用

當您將 R 程式碼從 R Studio 或另一個環境移至 SQL Server 時，通常將程式碼的運作方式不需要進一步修改時加入至 *@script* 參數[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 特別是如果您已經開發您的方案中使用**RevoScaleR**函式，因此相當簡單，變更執行內容。

不過，為了利用與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的更緊密整合，以及避免昂貴的資料傳輸成本，通常您會想要修改 R 程式碼以在 SQL Server 中執行。

若要檢視 R 程式碼如何在 SQL Server 中執行的範例，請參閱下列逐步解說：

+ [資料庫在分析 SQL 開發人員](../tutorials/sqldev-in-database-r-for-sql-developers.md)示範如何讓您的 R 程式碼更模組化其包裝在預存程序

+ [端對端資料科學方案](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)R 和 T-SQL 中包含的功能工程比較

## <a name="how-the-data-science-process-changes-in-sql-server"></a>資料科學程序如何變更 SQL Server 中

當您使用專用的 R 開發環境中這類[!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)]或 RStudio、 一般工作流程資料提取到您的電腦、 反覆，分析資料然後寫出或顯示結果。 不過，當您獨立 R 程式碼移轉至 SQL Server，此程序的許多簡化或委派給其他 SQL Server 工具。 此外，這樣做可以改善效能，在許多情況下。

| 外部程式碼 | SQL Server 中的 R |
|-------|-------|
| 內嵌資料| 定義輸入的資料做為 SQL 查詢。 避免資料移動。 |
| 對資料進行摘要並視覺化| 繪圖可以匯出為影像或傳送至遠端工作站。|
|特徵工程| 如果您不想要變更您的程式碼，但查看查詢最佳化，請使用 R 中的資料庫。 調查是否會更有效率的方式呼叫 T-SQL 函數或自訂的 Udf。|
|分析程序的資料清理部分| 執行特徵設計、 擷取特徵，以及資料清理事先做為資料工作流程的一部分。|
|將預測輸出至檔案| 將預測輸出至資料表，以避免資料移動。 自動換行預測直接存取的預存程序中的函式，藉由將應用程式。|

## <a name="best-practices"></a>最佳做法

+ 事先記下相依性 (例如必要的套件)。 在開發和測試環境中，在安裝您的程式碼時一併安裝套件或許是可行的方式，但在生產環境中則是一個不好的做法。 通知系統管理員，以便在部署程式碼之前，先安裝和測試套件。

+ 建立可能資料類型問題的檢查清單。 文件結構描述的程式碼的每個區段中預期的結果。

+ 識別主要資料來源 (例如模型訓練資料或預測用的輸入資料) 與次要來源 (例如因數、額外的分組變數等等) 的比較。 將您最大的資料集對應到 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的輸入參數。

+ 變更您的輸入資料陳述式以直接在資料庫中運作。 而不是將資料移到本機的 CSV 檔案，或進行重複呼叫 ODBC，您可以取得更佳的效能使用 SQL 查詢或檢視，可以直接對資料庫執行避免資料移動。

+ 使用 SQL Server 查詢計劃來識別可平行執行的工作。 如果輸入的查詢可以平行處理，設定`@parallel=1`做為您的引數的一部分[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 只要 SQL Server 可以與資料分割資料表搭配運作，或在多個處理序之間分散查詢並在最後彙總結果，通常就可以使用此旗標來進行平行處理。

  如果您使用要求讀取所有資料的演算法來訓練模型，或是您需要建立彙總，則通常無法使用此旗標來進行平行處理。

+ 請儘可能以支援分散式執行的 **ScaleR** 函數取代傳統 R 函數。 如需詳細資訊，請參閱[比較的基底 R 和小數位數的 R 函數](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler-compared-to-base-r)。

+ 檢閱您的 R 程式碼，以判斷是否有步驟可藉由使用個別的預存程序呼叫，來獨立執行或以更有效率的方式執行。 例如，您可能會決定將特徵工程或特徵擷取分開執行，並在新的資料行中新增值。 

  集合式計算，請使用 T-SQL，而不是 R 程式碼。 如需適用於功能工程工作比較 Udf 和 R 的 R 解決方案的範例，請參閱[資料科學端對端逐步解說](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)。

+ 使用 R 封裝**sqlrutils**若要將您的程式碼轉換成具有明確定義的輸入和輸出，可以輕易地對應至預存程序參數的單一函式。 如需詳細資訊和範例，請參閱[SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)。


## <a name="restrictions"></a>限制

 轉換 R 程式碼時，請將下列限制謹記在心：

### <a name="data-types"></a>資料類型

-   支援所有 R 資料類型。 不過，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援的資料類型比 R 更多樣，因此將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料傳送給 R (和反向傳送) 時，會執行一些隱含的資料類型轉換。 您也可能需要明確轉型或轉換部分資料。

- 支援 NULL 值。 使用 R`na`來表示遺漏值，類似於 null 的資料建構。

如需詳細資訊，請參閱[R 程式庫和資料型別](../r/r-libraries-and-data-types.md)。

### <a name="inputs-and-outputs"></a>[指令碼轉換編輯器]

+ 您只能定義一個輸入資料集來作為預存程序參數的一部分。 這個預存程序的輸入查詢可以是任何有效的單一 SELECT 陳述式。 我們建議您使用此輸入的最大的資料集，並取得較小的資料集，視需要使用 RODBC 呼叫。

+ 加上執行的預存程序呼叫不能做為輸入[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 輸入資料集內的所有資料行都必須與 R 指令碼中的變數對應。 變數會自動依名稱對應。 例如，假設您的 R 指令碼包含公式與下列類似：
    
    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
     如果輸入資料集不包含具有相符名稱 ArrDelay、 CRSDepTime、 DayOfWeek、 CRSDepHour 和 DayOfWeek 資料行，會引發錯誤。

+ 您也可以提供多個純量參數來作為輸入。 不過，任何您以 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 預存程序參數形式傳送的變數，都必須與 R 程式碼中的變數對應。 變數預設會依名稱對應。

+ 若要將純量輸入變數包含在 R 程式碼的輸出中，只要在定義變數時附加 **OUTPUT** 關鍵字即可。

+ 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中，您的 R 程式碼僅限以 data.frame 物件的形式輸出單一資料集。 不過，您也可以輸出多個純量輸出，包括二進位格式的繪圖及各種格式的模型。

+ 通常只要藉由使用 WITH RESULT SETS UNDEFINED 選項，即可輸出 R 指令碼所傳回的資料集，而不需指定輸出資料行的名稱。 不過，R 指令碼中任何您想要輸出的變數都必須與 SQL 輸出參數對應。

+ 如果您的 R 指令碼使用引數 `@parallel=1`，您就必須定義輸出結構描述。 這是因為 SQL Server 可能建立多個處理序來平行執行查詢，並在最後收集結果。 因此，才能建立平行處理，必須定義輸出結構描述。

### <a name="dependencies"></a>相依性

 + 避免從 R 程式碼安裝套件。 SQL Server 上應該預先安裝套件。
 
  請務必將封裝安裝到機器學習服務所使用的預設套件程式庫。 如需詳細資訊，請參閱[for SQL Server 的 R 封裝管理](../r/r-package-management-for-sql-server-r-services.md)
