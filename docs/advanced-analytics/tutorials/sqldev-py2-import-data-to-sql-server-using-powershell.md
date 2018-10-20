---
title: 步驟 2 將資料匯入 SQL Server 使用 PowerShell |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f8b90a18c0cdce9c4c2c73db4b599e488570f018
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461864"
---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>步驟 2： 將資料匯入 SQL Server 使用 PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是教學課程中，部分[適用於 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步驟中，您會執行其中一個已下載的指令碼，以建立本逐步解說所需的資料庫物件。 指令碼也會建立數個預存程序，並將範例資料上傳至您指定的資料庫中的資料表。

## <a name="create-database-objects-and-load-data"></a>建立資料庫物件並載入資料

在下載的檔案您應該會看到 PowerShell 指令碼， `RunSQL_SQL_Walkthrough.ps1`。 此指令碼的目的是要準備本逐步解說的環境。

指令碼會執行下列動作：

- 如果尚未安裝，請安裝 SQL Native Client 和 SQL 命令列公用程式。 使用 **bcp**將資料大量載入資料庫時，需要這些公用程式。

- 建立資料庫和資料表上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，並將資料大量插入至資料表。

- 建立多個 SQL 函式和預存程序。

如果您遇到問題時，您可以使用做為參考的指令碼手動執行步驟。

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>修改指令碼，以使用受信任的 Windows 身分識別

根據預設，指令碼會假設 SQL Server 資料庫使用者登入和密碼。 如果您是 db_owner Windows 使用者帳戶時，您可以使用您的 Windows 身分識別建立的物件。 若要這樣做，請開啟`RunSQL_SQL_Walkthrough.ps1`中要附加的程式碼編輯器**`-T`** bcp 大量插入命令：

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script"></a>執行指令碼

1. 以系統管理員身分開啟 PowerShell 命令提示字元。 如果您已不在上一個步驟中建立的資料夾中，瀏覽至資料夾，並接著執行下列命令：
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```

2. 指令碼會提示輸入下列資訊：

    - 名稱或位址[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]已經安裝 python 的 Machine Learning 服務的執行個體。
    - 執行個體上之帳戶的使用者名稱和密碼。 您使用的帳戶必須能夠建立資料庫、 建立資料表和預存程序，並大量載入資料至資料表。 
    - 如果您未提供使用者名稱和密碼，您的 Windows 身分識別用來登入 SQL Server。
    - 您剛才下載之範例資料檔案的路徑和檔案名稱。 例如： `C:\temp\pysql\nyctaxi1pct.csv` 

    > [!NOTE]
    > 若要成功地載入資料，程式庫 xmlrw.dll 必須 bcp.exe 相同資料夾中。

3. 指令碼也會修改[!INCLUDE[tsql](../../includes/tsql-md.md)]提供指令碼您稍早下載，並取代預留位置取代為資料庫名稱和使用者名稱。
  
4. 指令碼完成時，登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]函式使用指定驗證的資料庫、 資料表、 登入的執行個體，且已建立預存程序。 下圖顯示中的物件[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。

    ![瀏覽在 SSMS 中的資料表](media/sqldev-python-browsetables1.png "在 SSMS 中檢視資料表")

    > [!NOTE]
    > 如果資料庫物件已存在，它們不會再次建立。
    > 
    > 如果現有的資料表相同的名稱和結構描述的找到，則資料會附加而不會覆寫。 因此，請確定要卸除或截斷現有的資料表，然後執行指令碼。

## <a name="list-of-stored-procedures-and-functions"></a>預存程序和函式的清單

指令碼會建立下列的 SQL Server 物件：

|**SQL 指令碼檔案名稱**|**函數**|
|------|------|
|create-db-tb-upload-data.sql|建立資料庫和兩個資料表：<br /><br />nyctaxi_sample︰包含主要紐約市計程車資料集。 叢集資料行存放區索引會加入資料表，以提升儲存體和查詢效能。 紐約市計程車資料集的 1% 樣本會插入此資料表。<br /><br />nyc_taxi_models︰用來保存所定型的進階分析模型。|
|fnCalculateDistance.sql|建立純量值函式，以計算上車與下車位置之間的直線距離|
|fnEngineerFeatures.sql|建立資料表值函式，以建立用於定型模型的新資料特徵|
|TrainingTestingSplit.sql|Nyctaxi_sample 資料表中的資料分成兩個部分： nyctaxi_sample_training 和 nyctaxi_sample_testing。|
|PredictTipSciKitPy.sql|建立預存程序的呼叫所定型的模型 (scikit-learn-了解) 使用模型來建立預測。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。|
|PredictTipRxPy.sql|建立呼叫所定型的模型 (revoscalepy) 來使用模型建立預測的預存程序。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。|
|PredictTipSingleModeSciKitPy.sql|建立預存程序的呼叫所定型的模型 (scikit-learn-了解) 使用模型來建立預測。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。|
|PredictTipSingleModeRxPy.sql|建立呼叫所定型的模型 (revoscalepy) 來使用模型建立預測的預存程序。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。|

在本逐步解說的第二個部分中，您可以建立這些額外的預存程序：
    
|**SQL 指令碼檔案名稱**|**函數**|
|------|------|
|SerializePlots.sql|建立預存程序進行資料瀏覽。 這個預存程序來建立圖形使用 Python，然後將圖形物件序列化。|
|TrainTipPredictionModelSciKitPy.sql|建立訓練羅吉斯迴歸模型的預存程序 (scikit-learn-了解)。 模型會預測已支付小費的資料行的值，而且使用隨機選取的 60%的資料定型。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。|
|TrainTipPredictionModelRxPy.sql|建立訓練羅吉斯迴歸模型 (revoscalepy) 的預存程序。 模型會預測已支付小費的資料行的值，而且使用隨機選取的 60%的資料定型。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。|

## <a name="next-step"></a>下一步

[步驟 3：瀏覽及視覺化資料](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>上一個步驟

[步驟 1︰下載範例資料](demo-data-nyctaxi-in-sql.md)

