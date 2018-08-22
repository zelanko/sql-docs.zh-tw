---
title: 下載適用於內嵌 R (SQL Server Machine Learning) 的 NYC 計程車示範資料和指令碼 |Microsoft Docs
description: 指示下載紐約市計程車資料的範例，並建立資料庫。 在 SQL Server 教學課程示範如何內嵌 R 在 SQL Server 預存程序和 T-SQL 函式會使用資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: aca4450bdc152449fd30e974305d14a4ccbf77c5
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395065"
---
# <a name="load-nyc-taxi-demo-data-for-sql-server-tutorials"></a>NYC 計程車示範資料載入 SQL Server 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章會準備您的系統，如需如何使用 SQL Server 中的資料庫內分析的 R 教學課程。

在此練習中，您將會下載範例資料，準備環境，所需的 PowerShell 指令碼和[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼在數個教學課程中使用的檔案。 當您完成時， **NYCTaxi_Sample**資料庫位於本機執行個體，提供示範資料以進行實際操作學習。 

## <a name="prerequisites"></a>先決條件

您需要網際網路連線、 PowerShell 和的電腦上的本機系統管理權限。 您應該[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)或其他工具來驗證物件建立。

## <a name="download-nyc-taxi-demo-data-and-scripts-from-github"></a>從 Github 下載 NYC 計程車示範資料和指令碼

1.  開啟 Windows PowerShell 命令主控台。
  
    如果需要系統管理權限來建立目的地目錄，或將檔案寫入指定的目的地，請使用 [以系統管理員​​身分執行] 選項。
  
2.  執行下列 PowerShell 命令，將參數 *DestDir* 的值變更為任何本機目錄。  我們在此處使用的預設值是 **TempRSQL**。
  
    ```ps
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’
    ```
  
    如果您在 *DestDir* 中指定的資料夾不存在，PowerShell 指令碼就會加以建立。
  
    > [!TIP]
    > 如果您收到錯誤，可藉由使用略過引數，並訂出目前工作階段變更的範圍，以僅針對這個逐步解說，將執行 PowerShell 指令碼的原則暫時設為 **不受限制** 。
    >   
    >````
    > Set\-ExecutionPolicy Bypass \-Scope Process
    >````
    > 執行此命令不會導致設定變更。
  
    按照網際網路的連線速度，下載可能需要一些時間。
  
3.  當所有檔案皆已下載時，PowerShell 指令碼會開啟  *DestDir*所指定的資料夾。 在 PowerShell 命令提示字元中，執行下列命令，並檢閱已下載的檔案。
  
    ```
    ls
    ```
  
    **結果：**
  
    ![PowerShell 指令碼下載的檔案清單](media/rsql-devtut-filelist.png "PowerShell 指令碼下載的檔案清單")

## <a name="create-nyctaxisample-database"></a>建立 NYCTaxi_Sample 資料庫

在下載的檔案，您應該會看到 PowerShell 指令碼 (**RunSQL_SQL_Walkthrough.ps1**)，建立資料庫，並大量載入資料。 指令碼所執行的動作包括：

+ 如果尚未安裝，請安裝 SQL Native Client 和 SQL 命令列公用程式。 使用 **bcp**將資料大量載入資料庫時，需要這些公用程式。

+ 建立資料庫和資料表上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，並大量插入資料來源從.csv 檔案。

+ 建立多個 SQL 函數，以及數個教學課程中使用的預存程序。

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>修改指令碼，以使用受信任的 Windows 身分識別

根據預設，指令碼會假設 SQL Server 資料庫使用者登入和密碼。 如果您是 db_owner Windows 使用者帳戶時，您可以使用您的 Windows 身分識別建立的物件。 若要這樣做，請開啟`RunSQL_SQL_Walkthrough.ps1`程式碼編輯器中並附加**`-T`** bcp 大量插入命令 （行 238）：

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>執行指令碼來建立物件

在 C:\tempRSQL 中使用系統管理員的 PowerShell 命令提示字元，執行下列命令。
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
系統會提示您輸入下列資訊：

- 伺服器執行個體[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]已安裝。 在預設執行個體，這可以是簡單，只要電腦名稱。

- 資料庫名稱。 本教學課程中，指令碼假設`TaxiNYC_Sample`。

- 使用者名稱和使用者密碼。 輸入這些值的 SQL Server 資料庫登入。 或者，如果您修改要接受信任的 Windows 身分識別的指令碼，按 Enter，以將這些值保留為空白。 您的 Windows 身分識別用於連接。

- 在上一課中所下載的範例資料的完整的檔案名稱。 例如： `C:\tempRSQL\nyctaxi1pct.csv`

您提供這些值之後，立即執行指令碼。 指令碼在執行期間中的所有預留位置名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼已更新為使用您提供的輸入。

## <a name="review-database-objects"></a>檢閱資料庫物件
   
指令碼執行完成時，確認資料庫物件上存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 您應該會看到資料庫、 資料表、 函數和預存程序。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> 如果資料庫物件已存在，就無法再次建立。
>   
> 如果資料表已存在，則會附加而不是覆寫資料。 因此，請務必捨棄任何現有的物件，再執行指令碼。

### <a name="objects-in-nyctaxisample-database"></a>NYCTaxi_Sample 資料庫中的物件

下表摘要說明在 NYC 計程車示範資料庫中建立的物件。 雖然您只執行某個 PowerShell 指令碼 (`RunSQL_SQL_Walkthrough.ps1`)，該指令碼會呼叫其他的 SQL 指令碼，以建立您的資料庫中的物件。 用來建立每個物件的指令碼會在描述中所述。

|**物件名稱**|**物件類型**|**說明**|
|----------|------------------------|---------------|
|**TaxiNYC_Sample** | [資料庫] |建立-db-tb-上傳-data.sql 指令碼建立。 建立資料庫和兩個資料表：<br /><br />dbo.nyctaxi_sample 資料表： 包含主要紐約市計程車資料集。 叢集資料行存放區索引會加入資料表，以提升儲存體和查詢效能。 NYC 計程車資料集的 1%樣本會插入此資料表。<br /><br />dbo.nyc_taxi_models 資料表： 用來保存定型的進階的分析模型。|
|**fnCalculateDistance** |純量值函式 | FnCalculateDistance.sql 指令碼建立。 計算上車與下車位置之間的直線距離。 此函式會在[建立資料特徵](sqldev-create-data-features-using-t-sql.md)，[定型及儲存模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)並[R 模型作業化](sqldev-operationalize-the-model.md)。|
|**fnEngineerFeatures** |資料表值函式 | FnEngineerFeatures.sql 指令碼建立。 建立新的資料特徵來訓練模型。 此函式會在[建立資料特徵](sqldev-create-data-features-using-t-sql.md)並[R 模型作業化](sqldev-operationalize-the-model.md)。|
|**PlotHistogram** |預存程序 | PlotHistogram.sql 指令碼建立。 呼叫 R 函數，以繪製變數的長條圖，然後傳回繪圖作為二進位物件。 這個預存程序會在[瀏覽及視覺化資料](sqldev-explore-and-visualize-the-data.md)。|
|**PlotInOutputFiles** |預存程序| PlotInOutputFiles.sql 指令碼建立。 建立使用 R 函數的圖形，並接著會將輸出儲存為本機 PDF 檔案。 這個預存程序會在[瀏覽及視覺化資料](sqldev-explore-and-visualize-the-data.md)。|
|**PersistModel** |預存程序 | PersistModel.sql 指令碼建立。 接受已序列化為 varbinary 資料類型，並將它寫入至指定資料表的模型。 |
|**PredictTip**  |預存程序 |PredictTip.sql 指令碼建立。 呼叫所定型的模型，來使用模型建立預測。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。 這個預存程序會在[使 R 模型作業化](sqldev-operationalize-the-model.md)。|
|**PredictTipSingleMode**  |預存程序| PredictTipSingleMode.sql 指令碼建立。 呼叫所定型的模型，來使用模型建立預測。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。 這個預存程序會在[使 R 模型作業化](sqldev-operationalize-the-model.md)。|
|**TrainTipPredictionModel**  |預存程序|TrainTipPredictionModel.sql 指令碼建立。 藉由呼叫 R 封裝，可訓練羅吉斯迴歸模型。 此模型會預測已支付小費資料行的值，並使用隨機選取的 70%資料進行定型。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。 這個預存程序會在[定型及儲存模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)。|

## <a name="next-steps"></a>後續步驟

NYC 計程車資料範例現在可供實際操作學習。

+ [了解在 SQL Server 中使用 R 的資料庫內分析](sqldev-in-database-r-for-sql-developers.md)