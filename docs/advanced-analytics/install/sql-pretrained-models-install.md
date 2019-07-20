---
title: 安裝預先定型的機器學習模型
description: 將預先定型的模型用於情感分析, 並將影像特徵化新增至 SQL Server 2017 Machine Learning 服務 (R 或 Python) 或 SQL Server 2016 R 服務。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2045d6611d5f418a9ed102a1d776080973c08659
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344966"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>在 SQL Server 上安裝預先定型的機器學習模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何使用 Powershell 將*情感分析*和*影像特徵化*的免費預先定型機器學習模型新增至具有 R 或 Python 整合的 SQL Server 實例。 預先定型的模型是由 Microsoft 所建立並可立即使用, 並新增至實例做為後續安裝工作。 如需這些模型的詳細資訊, 請參閱本文的[資源](#bkmk_resources)一節。

安裝完成後, 預先定型的模型會被視為 MicrosoftML (R) 和 MicrosoftML (Python) 程式庫中特定功能的執行詳細資料。 您不應該 (也不能) 查看、自訂或重新定型模型, 也不能將它們視為自訂程式碼中的獨立資源或配對其他函數。 

若要使用預先定型模型, 請呼叫下表所列的函數。

| R 函式 (MicrosoftML) | Python 函式 (microsoftml) | 使用量 |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | 在文字輸入上產生正負情感分數。 |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 從影像檔案輸入中解壓縮文字資訊。 |

## <a name="prerequisites"></a>必要條件

機器學習演算法需要大量計算。 針對低至中等的工作負載, 我們建議使用 16 GB 的 RAM, 包括完成使用所有範例資料的教學課程逐步解說。

您必須擁有電腦的系統管理員許可權, 並 SQL Server 新增預先定型的模型。

必須啟用外部腳本, 且 SQL Server 啟動列服務必須執行。 安裝指示提供啟用和驗證這些功能的步驟。 

[MicrosoftML R package](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)或[MicrosoftML Python package](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)包含預先定型的模型。

+ [SQL Server 2017 Machine Learning 服務](sql-machine-learning-services-windows-install.md)同時包含機器學習程式庫的語言版本, 因此您不需採取任何進一步的動作, 就能符合此先決條件。 因為程式庫存在, 所以您可以使用本文中所述的 PowerShell 腳本, 將預先定型的模型新增至這些程式庫。

+ [SQL Server 2016 r 服務](sql-r-services-windows-install.md)(僅限 r) 不包含現成的[MicrosoftML 套件](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)。 若要新增 MicrosoftML, 您必須執行[元件升級](../install/upgrade-r-and-python.md)。 元件升級的其中一個優點是您可以同時新增預先定型的模型, 讓您不需要執行 PowerShell 腳本。 不過, 如果您已升級, 但第一次又錯過加入預先定型的模型, 您可以依照本文所述執行 PowerShell 腳本。 這適用于這兩個版本的 SQL Server。 在您執行之前, 請確認 MicrosoftML 程式庫存在於 C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library.


<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>檢查是否已安裝預先定型的模型

R 和 Python 模型的安裝路徑如下所示:

+ 針對 R:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ 針對 Python:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

模型檔案名如下所列:

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_ 101\_已更新。模型
+ ResNet\_ 18\_已更新。模型
+ ResNet\_50\_Updated.model

如果已安裝模型, 請直接跳到[驗證步驟](#verify)以確認可用性。

## <a name="download-the-installation-script"></a>下載安裝腳本

按一下[https://aka.ms/mlm4sql](https://aka.ms/mlm4sql)以下載檔案**Install-MLModels**。

## <a name="execute-with-elevated-privileges"></a>以更高的許可權執行

1. 啟動 PowerShell。 在工作列上, 以滑鼠右鍵按一下 PowerShell 程式圖示, 然後選取 [以**系統管理員身分執行**]。
2. 輸入安裝腳本檔案的完整路徑, 並包含實例名稱。 假設 [下載] 資料夾和預設實例, 命令可能如下所示:

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**輸出**

在連線到網際網路的 SQL Server 2017 Machine Learning 使用 R 和 Python 的預設實例, 您應該會看到類似下面的訊息。

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

首先, 檢查[mxlibs 資料夾](#file-location)中的新檔案。 接下來, 執行示範程式碼以確認模型已安裝且正常運作。 

### <a name="r-verification-steps"></a>R 驗證步驟

1. 開始**rgui.exe。** C:\Program FILES\MICROSOFT SQL Server\MSSQL14. 的 EXEMSSQLSERVER\R_SERVICES\bin\x64.

2. 在命令提示字元中, 貼上下列 R 腳本。

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

3. 按 Enter 以查看情感分數。 輸出應該如下所示:

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

1. 在 C:\Program Files\Microsoft SQL Server\MSSQL14. 啟動**Python .exe**MSSQLSERVER\PYTHON_SERVICES.

2. 在命令提示字元中, 貼上下列 Python 腳本

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

3. 按 Enter 鍵以列印分數。 輸出應該如下所示:

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> 如果示範腳本失敗, 請先檢查檔案位置。 在具有多個實例 SQL Server 或與獨立版本並存執行之實例的系統上, 安裝腳本可能會不正確地讀取環境, 並將檔案放在錯誤的位置。 通常, 手動將檔案複製到正確的 mxlib 資料夾會修正問題。

## <a name="examples-using-pre-trained-models"></a>使用預先定型模型的範例

下列連結包含叫用預先定型模型的範例程式碼。

+ [程式碼範例:使用文字 Featurizer 情感分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>研究和資源

目前可用的模型為情感分析和影像分類的深度類神經網路 (DNN) 模型。 所有預先定型的模型都是使用 Microsoft 的[計算網路工具](https://cntk.ai/Features/Index.html)組或**CNTK**來定型。

每個網路的設定都是以下列參考實作為基礎:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

如需這些深度學習模型中所使用之演算法的詳細資訊, 以及如何使用 CNTK 來執行和定型這些資料, 請參閱下列文章:

+ [Microsoft 研究人員的演算法設定 ImageNet 挑戰里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 計算網路工具組提供最有效率的分散式深度學習計算效能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>另請參閱

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning 服務](sql-machine-learning-services-windows-install.md)
+ [升級 SQL Server 實例中的 R 和 Python 元件](../install/upgrade-r-and-python.md)
+ [適用于 R 的 MicrosoftML 套件](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [適用于 Python 的 microsoftml 套件](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
