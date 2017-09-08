---
title: "步驟 2︰使用 PowerShell 將資料匯入 SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-vnext-ctp2
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62a06d6c442428132f84b3f8e5a665e872a8d361
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>步驟 2︰使用 PowerShell 將資料匯入 SQL Server

在此步驟中，您將執行其中一個下載的指令碼，建立本逐步解說所需的資料庫物件。 此指令碼也會建立您將會使用的大部分預存程序，並將範例資料上傳至您指定的資料庫資料表。

## <a name="create-sql-objects-and-data"></a>建立 SQL 物件和資料

在下載的檔案中，您應該會看到 PowerShell 指令碼。 為了準備本逐步解說的環境，您將執行此指令碼。  指令碼會執行下列動作：

- 如果尚未安裝，請安裝 SQL Native Client 和 SQL 命令列公用程式。 使用 **bcp**將資料大量載入資料庫時，需要這些公用程式。

- 在建立資料庫和資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，並將資料大量插入至資料表。

- 建立多個 SQL 函式和預存程序。

### <a name="run-the-script"></a>執行指令碼

1. 以系統管理員身分開啟 PowerShell 命令提示字元，然後執行下列命令。
  
    ```  
    .\RunSQL_SQL_Walkthrough.ps1  
    ```  

    系統會提示您輸入下列資訊：
    - 名稱或位址[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]已安裝的機器學習使用 Python 的服務執行個體
    - 執行個體上之帳戶的使用者名稱和密碼。 您使用的帳戶必須能夠建立資料庫、建立資料表和預存程序，以及將資料上傳至資料表。 如果您未提供使用者名稱和密碼，您的 Windows 身分識別用來登入 SQL Server。
    - 您剛才下載之範例資料檔案的路徑和檔案名稱。 例如，使用 IPv4 位址的 `C:\tempRSQL\nyctaxi1pct.csv`

    > [!NOTE]
    > 請確定您的 xmlrw.dll 您 bcp.exe 相同的資料夾。 如果沒有，請將它複製。

2.  在此步驟中，也會修改所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼，以您提供作為指令碼輸入的資料庫名稱和使用者名稱取代預留位置。
  
3. 請花幾分鐘檢閱指令碼所建立的預存程序和函數。
     
    |**SQL 指令碼檔案名稱**|**函數**|
    |------|------|
    |create-db-tb-upload-data.sql|建立資料庫和兩個資料表：<br /><br />nyctaxi_sample︰包含主要紐約市計程車資料集。 叢集資料行存放區索引會加入資料表，以提升儲存體和查詢效能。 紐約市計程車資料集的 1% 樣本會插入此資料表。<br /><br />nyc_taxi_models︰用來保存所定型的進階分析模型。|
    |fnCalculateDistance.sql|建立純量值函式，以計算上車與下車位置之間的直線距離|
    |fnEngineerFeatures.sql|建立資料表值函式，以建立用於定型模型的新資料特徵|
    |TrainingTestingSplit.sql|Nyctaxi_sample 資料表中的資料分成兩個部分： nyctaxi_sample_training 和 nyctaxi_sample_testing。|
    |PredictTipSciKitPy.sql|建立預存程序呼叫已定型的模型 (scikit-了解) 使用模型建立預測。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。|
    |PredictTipRxPy.sql|建立使用模型建立預測定型的模型 (revoscalepy) 會呼叫預存程序。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。|
    |PredictTipSingleModeSciKitPy.sql|建立預存程序呼叫已定型的模型 (scikit-了解) 使用模型建立預測。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。|
    |PredictTipSingleModeRxPy.sql|建立使用模型建立預測定型的模型 (revoscalepy) 會呼叫預存程序。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。|
  
4. 在本逐步解說後半部，您將建立一些額外的預存程序：
    
    |**SQL 指令碼檔案名稱**|**函數**|
    |------|------|
    |SerializePlots.sql|建立預存程序進行資料瀏覽。 這個預存程序建立圖形使用 Python，然後將圖形物件序列化。|
    |TrainTipPredictionModelSciKitPy.sql|建立羅吉斯迴歸模型定型的預存程序 (scikit-了解)。 模型在預測 （雪人） 的資料行的值，並經過定型，使用隨機選取的 60%的資料。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。|
    |TrainTipPredictionModelRxPy.sql|建立羅吉斯迴歸模型 (revoscalepy) 定型的預存程序。 模型在預測 （雪人） 的資料行的值，並經過定型，使用隨機選取的 60%的資料。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。|
  
3. 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 及您指定的登入，登入 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 執行個體，確認您可以看到已建立的資料庫、資料表、函數和預存程序。

    ![瀏覽在 SSMS 中的資料表](media/sqldev-python-browsetables1.png "在 SSMS 中檢視資料表")

    > [!NOTE]
    > 如果資料庫物件已存在，就無法再次建立。 如果資料表已存在，則會附加而不是覆寫資料。 因此，請務必捨棄任何現有的物件，再執行指令碼。
    > 請依照下列指示[這裡](https://docs.microsoft.com/en-us/sql/advanced-analytics/r/set-up-sql-server-r-services-in-database#bkmk_enableFeature)啟用外部指令碼服務。
    


## <a name="next-step"></a>下一個步驟

[步驟 3：瀏覽及視覺化資料](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>上一個步驟

[步驟 1︰下載範例資料](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>另請參閱

[使用 Python 的機器學習服務](../python/sql-server-python-services.md)



