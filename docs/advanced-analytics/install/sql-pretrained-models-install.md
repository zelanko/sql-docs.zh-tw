---
title: 安裝已訓練的模型
description: 將適用於情緒分析與影像特徵化的預先定型模型新增至 SQL Server Machine Learning 服務 (R 或 Python) 或 SQL Server R Services。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 97da2ed795d002fa47900eb21ead90b48b525387
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727556"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>在 SQL Server上安裝預先定型的機器學習模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此文章說明如何使用 Powershell 將適用於「情緒分析」  與「影像特徵化」  的預先定型免費機器學習模型新增到具有 R 或 Python 整合的 SQL Server 執行個體。 預先定型的模型是由 Microsoft 所建置並可立即使用，並新增至執行個體作為安裝後工作。 如需有關這些模型的詳細資訊，請參閱此文章的[資源](#bkmk_resources)一節。

安裝完成後，預先定型的模型會被視為支援 MicrosoftML (R) 與 MicrosoftML (Python) 程式庫中特定函式的實作詳細資料。 您不應該(也不能) 檢視、自訂或重新定型模型，也不能將它們視為自訂程式碼中的獨立資源或配對其他函式。 

若要使用預先定型的模型，請呼叫下表所列的函式。

| R 函式 (MicrosoftML) | Python 函式 (microsoftml) | 使用量 |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | 根據文字輸入產生正負情緒分數。 |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 從影像檔案輸入擷取文字資訊。 |

## <a name="prerequisites"></a>Prerequisites

機器學習演算法需要大量計算。 針對低至中等的工作負載 (包括使用所有範例資料完成教學課程逐步解說)，我們建議使用 16 GB 的 RAM。

您必須擁有電腦與 SQL Server 上的系統管理員權限，才能新增預先定型的模型。

必須啟用外部指令碼，而且 SQL Server LaunchPad 服務必須為執行中。 安裝指示提供啟用及驗證這些功能的步驟。 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[MicrosoftML R 套件](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)或 [microsoftml Python 套件](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)包含預先定型的模型。

[SQL Server 機器學習服務](sql-machine-learning-services-windows-install.md)同時包括機器學習程式庫的兩個語言版本，因此您不需採取任何進一步的動作，就能符合此先決條件。 因為程式庫存在，所以您可以使用此文章中所述的 PowerShell 指令碼將預先定型的模型新增到這些程式庫。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[MicrosoftML R 套件](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)包含預先定型的模型。

[SQL Server R Services](sql-r-services-windows-install.md) (僅限 R) 預設不包括 [MicrosoftML 套件](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)。 若要新增 MicrosoftML，您必須執行[元件升級](../install/upgrade-r-and-python.md)。 元件升級的其中一個優點是您可以同時新增預先定型的模型，讓您不需要執行 PowerShell 指令碼。 不過，如果您已升級，而且一開始錯過新增預先定型的模型，您可以依照此文章所述執行 PowerShell 指令碼。 這適用於兩個版本的 SQL Server。 在您執行之前，請確認 MicrosoftML 程式庫存在於 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`。
::: moniker-end

<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>檢查是否已安裝預先定型的模型

R 與 Python 模型的安裝路徑如下所示：

+ 針對 R：`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ 針對 Python：`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

模型檔案名稱如下所列：

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

若已安裝模型，請直接跳到[驗證步驟](#verify)以確認可用性。

## <a name="download-the-installation-script"></a>下載安裝指令碼

按一下 [https://aka.ms/mlm4sql](https://aka.ms/mlm4sql) 以下載 **Install-MLModels.ps1** 檔案。

## <a name="execute-with-elevated-privileges"></a>以提高的權限執行

1. 啟動 PowerShell。 在工作列上，以滑鼠右鍵按一下 PowerShell 程式圖示，然後選取 [以系統管理員身分執行]  。
2. 輸入安裝指令碼檔案的完整路徑，並包含執行個體名稱。 假設您使用 [下載] 資料夾與預設執行個體，命令看起來可能像下面這樣：

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**輸出**

在已連線到網際網路且具有 R 與 Python 的 SQL Server 機器學習服務預設執行個體上，您應該會看到像下面的訊息。

   ```powershell
   MSSQL14.MSSQLSERVER
        Verifying R models [9.2.0.24]
        Downloading R models [C:\Users\<user-name>\AppData\Local\Temp]
        Installing R models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\]
        Verifying Python models [9.2.0.24]
        Installing Python models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\]
   PS C:\WINDOWS\system32>
   ```

<a name="verify"> </a>

## <a name="verify-installation"></a>確認安裝

首先，檢查 [mxlibs 資料夾](#file-location)中的新檔案。 接下來，執行示範程式碼以確認模型已安裝且正常運作。 

### <a name="r-verification-steps"></a>R 驗證步驟

1. 啟動位於 C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64 的 **RGUI.EXE**。

2. 在命令提示字元中，貼上下列 R 指令碼。

    ```R
    # Create the data
    CustomerReviews <- data.frame(Review = c(
    "I really did not like the taste of it",
    "It was surprisingly quite good!",
    "I will never ever ever go to that place again!!"),
    stringsAsFactors = FALSE)

    # Get the sentiment scores
    sentimentScores <- rxFeaturize(data = CustomerReviews, 
                                    mlTransforms = getSentiment(vars = list(SentimentScore = "Review")))

    # Let's translate the score to something more meaningful
    sentimentScores$PredictedRating <- ifelse(sentimentScores$SentimentScore > 0.6, 
                                            "AWESOMENESS", "BLAH")

    # Let's look at the results
    sentimentScores
    ```

3. 按 Enter 以檢視情緒分數。 輸出應該如下所示：

    ```R
    > sentimentScores
                                            Review SentimentScore
    1           I really did not like the taste of it      0.4617899
    2                 It was surprisingly quite good!      0.9601924
    3 I will never ever ever go to that place again!!      0.3103435
    PredictedRating
    1            BLAH
    2     AWESOMENESS
    3            BLAH
    ```

### <a name="python-verification-steps"></a>Python 驗證步驟

1. 啟動位於 C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES 的 **Python.EXE**。

2. 在命令提示字元中，貼上下列 Python 指令碼

    ```python
    import numpy
    import pandas
    from microsoftml import rx_logistic_regression, rx_featurize, rx_predict, get_sentiment

    # Create the data
    customer_reviews = pandas.DataFrame(data=dict(review=[
                "I really did not like the taste of it",
                "It was surprisingly quite good!",
                "I will never ever ever go to that place again!!"]))
                
    # Get the sentiment scores
    sentiment_scores = rx_featurize(
        data=customer_reviews,
        ml_transforms=[get_sentiment(cols=dict(scores="review"))])
        
    # Let's translate the score to something more meaningful
    sentiment_scores["eval"] = sentiment_scores.scores.apply(
                lambda score: "AWESOMENESS" if score > 0.6 else "BLAH")
    print(sentiment_scores)
    ```

3. 按 Enter 以列印分數。 輸出應該如下所示：

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> 若示範指令碼失敗，請先檢查檔案位置。 在具有多個 SQL Server 執行個體或與獨立版本並存執行之執行個體的系統上，安裝指令碼可能會不正確地讀取環境，並將檔案放在錯誤的位置。 通常，手動將檔案複製到正確的 mxlib 資料夾即可修正問題。

## <a name="examples-using-pre-trained-models"></a>使用預先定型模型的範例

下列連結包含會叫用預先定型模型的範例程式碼。

+ [程式碼範例：使用文字 Featurizer 進行情感分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>研究與資源

目前可用的模型為適用於情緒分析與影像分類的深度類神經網路 (DNN) 模型。 所有預先定型的模型都是使用 Microsoft 的[計算網路工具組](https://cntk.ai/Features/Index.html) (或稱 **CNTK**) 來定型的。

每個網路的設定都是以下列參考實作為基礎：

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

如需有關這些深度學習模型中所使用之演算法，以及如何使用 CNTK 來加以執行及定型的詳細資訊，請參閱下列文章：

+ [Microsoft Researcher 的演算法集合 ImageNet 查問里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/) \(英文\)

+ [Microsoft 計算網路工具組提供最有效率的分散式深度學習計算效能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/) \(英文\)

## <a name="see-also"></a>另請參閱

+ [SQL Server Machine Learning 服務](sql-machine-learning-services-windows-install.md)
+ [升級 SQL Server 執行個體中的 R 與 Python 元件](../install/upgrade-r-and-python.md)
+ [ R 的 MicrosoftML 套件](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) \(英文\)
+ [ Python 的 microsoftml 套件](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) \(英文\)
