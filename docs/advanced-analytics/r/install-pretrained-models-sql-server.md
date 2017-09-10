---
title: "SQL Server 上安裝預先定型的機器學習模型 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14789bafd555a4980875de78c85b32f535a8c0fe
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>安裝預先定型的機器學習模型 SQL Server 上

本主題描述如何將預先定型的模型加入至 SQL Server 執行個體在具有 R 服務，或安裝的機器學習服務。

預先定型的模型會提供 Microsoft R Server （或更新 Microsoft Machine Learning 伺服器） 進行更新。 如需如何升級您的執行個體並取得最新版的 Microsoft R 資訊，請參閱[升級 R 服務執行個體中的 R 元件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

您可以執行 R Server 的個別 windows 安裝程式，只安裝這些模型。
不過，有一些額外的步驟來安裝 SQL Server 上的模型時所使用。 本主題描述處理程序。

## <a name="benefits-of-using-pretrained-models"></a>使用 預先定型的模型的優點

預先定型的模型已有可用來支援客戶需要執行工作，例如情緒分析，或安裝映像功能，其潛在，但不是需要的資源來取得大型資料集或複雜的模型定型。 使用預先定型的模型，可讓您開始文字和最有效率的方式處理映像。

目前可用的模型是情緒分析和影像分類的深度類神經網路 (DNN) 模型。 所有四個預先定型的模型已定型 CNTK。 每個網路的設定根據下列參考實作：

+ Resnet 18
+ Resnet 50
+ ResNet 101
+ AlexNet

如需深入剩餘的網路及使用 CNTK 其實作的詳細資訊，請參閱下列文章：

+ [Microsoft 研究人員演算法設定 ImageNet 挑戰里程碑](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 計算網路工具組提供最有效率的分散式的深層學習計算效能](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>如何安裝 SQL Server 上的模型

   > [!NOTE]
   > 
   > 如果要安裝 Microsoft R Server，或升級您的 SQL Server 執行個體，您可以使用個別的 windows 安裝程式，預先定型的模型都是從安裝程式。 請參閱[適用於 Windows 的安裝 R Server](https://docs.microsoft.com/en-us/r-server/install/r-server-install-windows)。
   > 
   > 若要使用模型與 Microsoft R Server，可能需要一些額外的步驟。 如需詳細資訊，請參閱[如何安裝和部署預先定型的機器學習模型與 MicrosoftML](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)

1. 當您安裝 SQL Server; 預先定型的模型不是預設安裝SQL Server 安裝程式完成之後執行安裝程式命令列公用程式，您必須將其加入。

2. 開啟提升權限的命令提示字元並瀏覽至安裝程式啟動載入器資料夾的 SQL Server，其中也包含 Microsoft R 安裝程式。

    在 SQL Server 2017 RC 1 的預設執行個體，這會是：
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017RC1\x64\`

3. 指定要安裝、 元件及預先定型的模型應在何處加入，使用下列引數的資料夾：

  + 若要使用模型與**R_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\R_SERVICES`

    例如，若要啟用 SQL Server 2017 的預設執行個體中使用 R 的預先定型模型，您會執行此陳述式：

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES"`

  + 若要使用模型與**PYTHON_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\PYTHON_SERVICES`

    比方說，若要啟用預先定型的模型使用 Python，預設執行個體的 SQL Server 2017，您會執行此陳述式：

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"`

4. 版本參數，支援下列值：

    + 發行候選版本 0: **9.1.0.0**
    + 候選版 1: **9.2.0.22**
    + 最終的版本號碼 （不會釋放）： **9.2.0.100**

5. 如果安裝成功，下列模型應加入至您的 R\_服務或 PYTHON\_SERVICES 資料夾：

    - AlexNet_Updated.model
    - ImageNet1K_mean.xml
    - pretrained.model
    - ResNet_101_Updated.model
    - ResNet_18_Updated.model
    - ResNet_50_Updated.model

## <a name="examples"></a>範例

您已安裝的模型之後，您可以使用模型從 R 程式碼呼叫的方式。

### <a name="image-featurization-example"></a>映像功能，其潛在範例

映像預先定型的模型支援功能，其潛在您提供的映像。 若要使用模型，您呼叫**featurizeImage**轉換。

+ [featurizeImage： 機器學習映像功能，其潛在轉換](https://docs.microsoft.com/r-server/r-reference/microsoftml/featurizeimage)

在此範例中，請參閱程式碼的第二個區塊。 載入影像時，調整大小，以及預先定型的 convolutional DNN 模型的特徵化。 DNN featurizer 輸出接著用於定型影像分類的線性模型。

影像必須調整大小以符合需求的定型的模型： 用於定型的影像時發生 224 x 224 像素。 如果您使用 AlexNet 模型，影像會調整大小以便 227 x 227 像素。

```R
 model <- rxFastLinear(
     Label ~ Features,
     data = train,
     mlTransforms = list(
         loadImage(vars = list(Features = "Path")),
         resizeImage(vars = "Features", width = 224, height = 224), 
         extractPixels(vars = "Features"),
         featurizeImage(var = "Features")
         ),
     mlTransformVars = "Path")
```

> [!NOTE]
> 
> 您不可以讀取或修改預先定型的模型本身。 這個特定模型根據[CNTK](https://docs.microsoft.com/cognitive-toolkit/)模型，但基於效能的考量中使用原生格式已經壓縮。

### <a name="text-analysis-example"></a>文字分析範例

這個範例示範用於分類的預先定型的模型：

[使用文字 Featurizer 情緒分析](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)
