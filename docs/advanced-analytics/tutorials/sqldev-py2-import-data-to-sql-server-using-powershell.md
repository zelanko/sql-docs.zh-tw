---
title: "步驟 2： 將資料匯入 SQL Server 使用 PowerShell |Microsoft 文件"
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: d39e391e494e37c63731431579e82900ef3dbeeb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>步驟 2： 將資料匯入 SQL Server 使用 PowerShell

這篇文章的教學課程中，屬於[SQL 開發人員的資料庫中的 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步驟中，您執行其中一個下載的指令碼，來建立這個逐步解說所需的資料庫物件。 指令碼也會建立數個預存程序，並將範例資料上傳至您指定的資料庫中的資料表。

## <a name="create-database-objects-and-load-data"></a>建立資料庫物件和載入資料

下載的檔案之間，您應該看到的 PowerShell 指令碼， `RunSQL_SQL_Walkthrough.ps1`。 此指令碼的目的是要準備逐步解說的環境。

指令碼會執行下列動作：

- 如果尚未安裝，請安裝 SQL Native Client 和 SQL 命令列公用程式。 使用 **bcp**將資料大量載入資料庫時，需要這些公用程式。

- 在建立資料庫和資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，並將資料大量插入至資料表。

- 建立多個 SQL 函式和預存程序。

如果您遇到問題時，您可以使用做為參考的指令碼手動執行步驟。

1. 以系統管理員身分開啟 PowerShell 命令提示字元。 如果您已不在上一個步驟中建立的資料夾中，瀏覽至資料夾，並執行下列命令：
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```

2. 指令碼會提示輸入下列資訊：

    - 名稱或位址[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]已安裝使用 Python 的機器學習服務執行個體。
    - 執行個體上之帳戶的使用者名稱和密碼。 您使用的帳戶必須具有建立資料庫、 建立資料表和預存程序，並大量載入資料至資料表的能力。 
    - 如果您未提供使用者名稱和密碼，您的 Windows 身分識別用來登入 SQL Server，而且您會提升輸入密碼。
    - 您剛才下載之範例資料檔案的路徑和檔案名稱。 例如，使用 IPv4 位址的 `C:\temp\pysql\nyctaxi1pct.csv`

    > [!NOTE]
    > 若要成功地載入資料時，程式庫 xmlrw.dll 必須 bcp.exe 相同資料夾中。

3. 指令碼也會修改[!INCLUDE[tsql](../../includes/tsql-md.md)]提供指令碼更早版本，您已下載，並取代預留位置取代的資料庫名稱和使用者名稱。
  
4. 指令碼完成時，登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]函式的執行個體使用指定驗證的資料庫資料表中的登入，且已建立預存程序。 下圖顯示在物件[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。

    ![瀏覽在 SSMS 中的資料表](media/sqldev-python-browsetables1.png "在 SSMS 中檢視資料表")

    > [!NOTE]
    > 如果已經存在的資料庫物件，而無法建立一次。
    > 
    > 如果現有的資料表相同的名稱和結構描述的發現，資料將會附加，不會覆寫。 因此，請確定要卸除或截斷現有的資料表，再執行指令碼。

## <a name="list-of-stored-procedures-and-functions"></a>預存程序和函數的清單

指令碼會建立下列的 SQL Server 物件：

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

在本逐步解說的第二個部分中，您可以建立這些額外預存程序：
    
|**SQL 指令碼檔案名稱**|**函數**|
|------|------|
|SerializePlots.sql|建立預存程序進行資料瀏覽。 這個預存程序建立圖形使用 Python，然後將圖形物件序列化。|
|TrainTipPredictionModelSciKitPy.sql|建立羅吉斯迴歸模型定型的預存程序 (scikit-了解)。 模型在預測 （雪人） 的資料行的值，並經過定型，使用隨機選取的 60%的資料。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。|
|TrainTipPredictionModelRxPy.sql|建立羅吉斯迴歸模型 (revoscalepy) 定型的預存程序。 模型在預測 （雪人） 的資料行的值，並經過定型，使用隨機選取的 60%的資料。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。|

## <a name="next-step"></a>下一步

[步驟 3：瀏覽及視覺化資料](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>上一個步驟

[步驟 1︰下載範例資料](sqldev-py1-download-the-sample-data.md)

