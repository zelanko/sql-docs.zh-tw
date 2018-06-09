---
title: 第 2 課準備 R 教學課程環境中使用 PowerShell （SQL Server 機器學習） |Microsoft 文件
description: 教學課程顯示如何在 SQL Server 中內嵌 R 預存程序和 T-SQL 函數
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1280d7c82d48c8ed596271cd7a73fa13ec1664c7
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249741"
---
# <a name="lesson-2-set-up-the-tutorial-environment-using-powershell"></a>第 2 課： 設定教學課程的環境使用 PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在此步驟中，您將執行 PowerShell 指令碼來建立這個逐步解說所需的資料庫物件。 指令碼會建立並載入資料庫，使用在上一個步驟中取得的範例資料。 它也會建立函式和預存程序教學課程中使用。

## <a name="create-and-load-database-objects"></a>建立並載入資料庫物件

在下載的檔案，您應該會看到的 PowerShell 指令碼 (`RunSQL_SQL_Walkthrough.ps1`)，會準備逐步解說的環境。 指令碼所執行的動作包括：

- 如果尚未安裝，請安裝 SQL Native Client 與 SQL 命令列公用程式。 使用 **bcp**將資料大量載入資料庫時，需要這些公用程式。

- 在建立資料庫和資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，並大量插入資料來源從.csv 檔案。

- 建立多個 SQL 函式和預存程序。

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>修改指令碼以使用受信任的 Windows 身分識別

根據預設，指令碼會假設 SQL Server 資料庫使用者登入和密碼。 如果您是 db_owner Windows 使用者帳戶時，您可以使用您的 Windows 身分識別來建立物件。 若要這樣做，請開啟`RunSQL_SQL_Walkthrough.ps1`程式碼編輯器中並附加**`-T`** bcp 大量插入命令 （行 238）：

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>執行指令碼來建立物件

以系統管理員身分開啟 PowerShell 命令提示字元，然後執行下列命令。
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
系統會提示您輸入下列資訊：

- 伺服器執行個體[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]已安裝。 上預設執行個體，這可以是簡單的電腦名稱。

- 資料庫名稱。 此教學課程中，指令碼會假設`TaxiNYC_Sample`。

- 使用者名稱和使用者密碼。 輸入這些值的 SQL Server 資料庫登入。 或者，如果您修改要接受受信任的 Windows 身分識別的指令碼，按 Enter，以將這些值保留空白。 您的 Windows 身分識別用於連接。

- 上一課中所下載的範例資料的完整的檔案名稱。 例如： `C:\tempRSQL\nyctaxi1pct.csv`

提供這些值之後，會立即執行指令碼。 指令碼在執行期間，在所有的預留位置名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼都會更新為使用您提供的輸入。

## <a name="review-database-objects"></a>檢閱資料庫物件
   
指令碼執行完成時，確認資料庫物件存在於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 您應該會看到資料庫、 資料表、 函數和預存程序。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> 如果資料庫物件已存在，就無法再次建立。
>   
> 如果資料表已存在，則會附加而不是覆寫資料。 因此，請務必捨棄任何現有的物件，再執行指令碼。

## <a name="objects-used-in-this-tutorial"></a>本教學課程中使用的物件

下表摘要說明在這一課建立的物件。 雖然您只執行一個 PowerShell 指令碼 (`RunSQL_SQL_Walkthrough.ps1`)，該指令碼會呼叫其他的 SQL 指令碼，接著，您的資料庫中建立的物件。 用來建立每個物件的指令碼會在描述中所述。

|**物件名稱**|**物件類型**|**說明**|
|----------|------------------------|---------------|
|**TaxiNYC_Sample** | [資料庫] |建立-db-tb-上傳-data.sql 指令碼建立。 建立資料庫和兩個資料表：<br /><br />dbo.nyctaxi_sample 資料表： 包含主要 NYC 計程車資料集。 叢集資料行存放區索引會加入資料表，以提升儲存體和查詢效能。 %1 的範例 NYC 計程車資料集被插入此資料表。<br /><br />dbo.nyc_taxi_models 資料表： 用於保存定型的進階的分析模型。|
|**fnCalculateDistance** |純量值函式 | 建立 fnCalculateDistance.sql 指令碼。 計算收取和 dropoff 位置之間的直接距離。 此函式用於[建立資料的功能](../tutorials/sqldev-create-data-features-using-t-sql.md)，[定型和儲存模型](sqldev-train-and-save-a-model-using-t-sql.md)和[實施 R 模型](../tutorials/sqldev-operationalize-the-model.md)。|
|**fnEngineerFeatures** |資料表值函式 | 建立 fnEngineerFeatures.sql 指令碼。 建立新的資料功能，進行模型定型。 此函式用於[建立資料的功能](../tutorials/sqldev-create-data-features-using-t-sql.md)和[實施 R 模型](../tutorials/sqldev-operationalize-the-model.md)。|
|**PlotHistogram** |預存程序 | 建立 PlotHistogram.sql 指令碼。 呼叫以繪製的長條圖，變數的 R 函數，並傳回繪圖當成二進位物件。 這個預存程序用於[探索和視覺化資料](../tutorials/sqldev-explore-and-visualize-the-data.md)。|
|**PlotInOutputFiles** |預存程序| 建立 PlotInOutputFiles.sql 指令碼。 建立使用的 R 函數的圖形，然後將輸出儲存為本機的 PDF 檔案。 這個預存程序用於[探索和視覺化資料](../tutorials/sqldev-explore-and-visualize-the-data.md)。|
|**PersistModel** |預存程序 | 建立 PersistModel.sql 指令碼。 會在 varbinary 資料類型中，已序列化，並將它寫入至指定資料表的模型。 |
|**PredictTip**  |預存程序 |建立 PredictTip.sql 指令碼。 呼叫已定型的模型使用模型建立預測。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。 這個預存程序用於[實施 R 模型](../tutorials/sqldev-operationalize-the-model.md)。|
|**PredictTipSingleMode**  |預存程序| 建立 PredictTipSingleMode.sql 指令碼。 呼叫已定型的模型使用模型建立預測。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。 這個預存程序用於[實施 R 模型](../tutorials/sqldev-operationalize-the-model.md)。|
|**TrainTipPredictionModel**  |預存程序|建立 TrainTipPredictionModel.sql 指令碼。 藉由呼叫 R 封裝培訓羅吉斯迴歸模型。 此模型會預測已支付小費資料行的值，並使用隨機選取的 70%資料進行定型。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。 這個預存程序用於[定型和儲存模型](sqldev-train-and-save-a-model-using-t-sql.md)。|

## <a name="next-lesson"></a>下一課

[第 3 課： 探索和視覺化資料](../tutorials/sqldev-explore-and-visualize-the-data.md)

## <a name="previous-lesson"></a>上一課

[第 1 課： 下載範例資料](../tutorials/sqldev-download-the-sample-data.md)
