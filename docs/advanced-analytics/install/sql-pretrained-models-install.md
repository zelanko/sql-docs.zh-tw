---
title: SQL Server 上安裝預先定型的機器學習服務模型 |Microsoft Docs
description: 加入 SQL Server 2017 Machine Learning 服務 （R 或 Python） 或 SQL Server 2016 R Services 的預先定型的情感分析和影像特徵化的模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/18/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b2dfee04a7c0c9c39b7969551a85a49d441f30e5
ms.sourcegitcommit: 84cc5ed00833279da3adbde9cb6133a4e788ed3f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2018
ms.locfileid: "39216829"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>安裝預先定型的機器學習服務模型在 SQL Server 上
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何使用 Powershell 來新增可用預先定型的機器學習服務模型*情感分析*並*影像特徵化*擁有 R 或 Python 的 SQL Server 資料庫引擎執行個體整合。 Microsoft 和已準備好上手，不會建立預先定型的模型加入至資料庫引擎執行個體做為後續安裝工作。 如需有關這些模型的詳細資訊，請參閱 <<c0> [ 資源](#bkmk_resources)一節。

安裝之後，預先定型的模型會被視為電源的 MicrosoftML (R) 和 microsoftml (Python) 程式庫中的特定函式的實作詳細資料。 您不應該 （而且也無法） 檢視、 自訂或重新定型模型，也可以您將它們視為獨立的資源，在自訂程式碼或配對的其他函式。 

若要使用預先定型的模型，請呼叫下表所列出的函數。

| R 函式 (MicrosoftML) | Python 函式 (microsoftml) | 使用方式 |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | 您可以產生正負面情感分數對文字輸入。 [了解更多](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)。|
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 從映像檔案輸入擷取文字資訊。 [了解更多](https://blogs.msdn.microsoft.com/mlserver/2017/04/12/image-featurization-with-a-pre-trained-deep-neural-network-model/)。 |

## <a name="prerequisites"></a>先決條件

機器學習演算法會耗用大量運算資源。 我們建議針對低到中等的工作負載，包括使用的所有範例資料的教學課程逐步解說完成的 16 GB RAM。

您必須擁有系統管理員權限的電腦和 SQL Server，將預先定型的模型。

必須啟用外部指令碼，您必須執行 SQL Server LaunchPad 服務。 安裝指示會提供啟用和驗證這些功能的步驟。 

[MicrosoftML R 封裝](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)或是[microsoftml Python 封裝](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)包含預先定型的模型。

+ [SQL Server 2017 Machine Learning 的服務](sql-machine-learning-services-windows-install.md)包含這兩個語言版本的機器學習服務程式庫中，讓您採取任何進一步的動作不滿足這項必要條件。 因為存在程式庫，您可以使用本文中所述的 PowerShell 指令碼，將這些程式庫中的預先定型的模型。

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)，這是 R，不包括[MicrosoftML 套件](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)現成的。 若要新增 MicrosoftML，您必須執行[元件升級](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。 元件升級的優點之一是，您可以同時新增預先定型的模型，這可讓執行不必要的 PowerShell 指令碼。 不過，如果您已經升級，但遺漏了第一次新增預先定型的模型，您可以執行 PowerShell 指令碼，如這篇文章中所述。 它適用於這兩個版本的 SQL Server。 這麼做之前，請確認 MicrosoftML 程式庫會位於 C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library。


<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>檢查是否已安裝預先定型的模型

R 和 Python 模型的安裝路徑，如下所示：

+ R `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ 適用於 Python: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs `

模型檔案名稱如下所示：

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

如果已安裝的模型，則請直接跳到[驗證步驟](#verify)以確認。

## <a name="download-the-installation-script"></a>下載安裝指令碼

按一下  [ https://aka.ms/mlm4sql ](https://aka.ms/mlm4sql)來下載檔案**安裝 MLModels.ps1**。

## <a name="execute-with-elevated-privileges"></a>使用提高的權限執行

1. 啟動 PowerShell。 在工作列上，以滑鼠右鍵按一下 [PowerShell] 程式圖示，然後選取**系統管理員身分執行**。
2. 輸入完整路徑，安裝指令碼檔案，並包含執行個體名稱。 假設 [下載] 資料夾和預設執行個體，此命令可能會看起來像這樣：

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**輸出**

連線到網際網路的 SQL Server 2017 Machine Learning 預設執行個體上使用 R 和 Python，您應該會看到類似下列的訊息。

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

首先，檢查新的檔案中[mxlibs 資料夾](#file-location)。 接下來，執行示範程式碼，以確認這些模型都已安裝且運作正常。 

### <a name="r-verification-steps"></a>R 驗證步驟

1. 啟動**RGUI。EXE**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\R_SERVICES\bin\x64。

2. 在下列的 R 指令碼，在命令提示字元中，貼上。

    ```r
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

3. 按下 Enter，以檢視情感分數。 輸出應如下所示：

    ```
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

1. 開始**Python.exe**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES。

2. 下列 Python 指令碼，在命令提示字元中貼上

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

3. 按 Enter 鍵，列印分數。 輸出應如下所示：

    ```
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> 如果示範指令碼失敗，請先檢查檔案的位置。 在系統上有多個 SQL Server 執行個體，或執行個體執行的並行與獨立版本，可能會安裝指令碼錯誤讀取環境，並將檔案放在錯誤的位置。 通常，手動將檔案複製到正確的 mxlib 資料夾即可修正問題。

## <a name="examples-using-pre-trained-models"></a>使用預先定型的模型範例

以下連結包括叫用預先定型的模型中的逐步解說和範例程式碼。

+ [在 SQL Server Machine Learning 服務中使用 Python 的情感分析](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

+ [使用預先定型的深度類神經網路模型的影像特徵化](https://blogs.msdn.microsoft.com/mlserver/2017/04/12/image-featurization-with-a-pre-trained-deep-neural-network-model/)

  預先定型的模型，針對映像支援您所提供的映像的功能。 若要使用模型，請呼叫**featurizeImage**轉換。 載入影像時，調整大小，並使用定型模型。 DNN featurizer 的輸出則用於定型影像分類的線性模型。 若要使用此模型中，所有映像必須調整大小以符合需求的定型模型。 例如，如果您使用的 AlexNet 模型時，映像應該能調整 227 x 227 像素。

+ [程式碼範例： 使用文字 Featurizer 情感分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>參考資料和資源

目前可用的模型是情感分析和影像分類的深度類神經網路 (DNN) 模型。 所有預先定型的模型使用 Microsoft 的定型[運算網路工具組](https://cntk.ai/Features/Index.html)，或**CNTK**。

每個網路的設定根據下列的參考實作：

+ ResNet 18
+ ResNet 50
+ ResNet-101
+ AlexNet

如需有關演算法用在這些深入學習模型，以及其實作方式及使用 CNTK 的訓練，請參閱下列文章：

+ [Microsoft 研究人員的演算法會將 ImageNet 挑戰里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [運算網路工具組 Microsoft 提供最有效率的分散式的深度學習的計算效能，](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>另請參閱

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning 服務](sql-machine-learning-services-windows-install.md)
+ [升級 SQL Server 執行個體中的 R 和 Python 元件](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
+ [適用於 R 的 MicrosoftML 套件](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [適用於 Python 的 microsoftml 套件](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
