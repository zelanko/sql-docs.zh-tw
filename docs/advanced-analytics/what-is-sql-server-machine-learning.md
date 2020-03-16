---
title: 什麼是 SQL Server 機器學習服務 (Python 和 R)？
titleSuffix: ''
description: 機器學習服務是 SQL Server 內的一項功能，能夠使用關聯式資料執行 Python 和 R 指令碼。 您可以使用開放原始碼套件和架構，以及 Microsoft Python 和 R 套件，來進行預測性分析與機器學習。 指令碼會在資料庫中執行，不需在 SQL Server 外部或透過網路來移動資料。 本文說明 SQL Server 機器學習服務的基本概念。
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/06/2020
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a94a3aea418a4c404b568fe6df7af701bc46de34
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79285902"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>什麼是 SQL Server 機器學習服務 (Python 和 R)？
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

機器學習服務是 SQL Server 內的一項功能，能夠使用關聯式資料執行 Python 和 R 指令碼。 您可以使用開放原始碼套件和架構，以及 [Microsoft Python 和 R 套件](#packages)，來進行預測性分析與機器學習。 指令碼會在資料庫中執行，不需在 SQL Server 外部或透過網路來移動資料。 本文說明 SQL Server 機器學習服務的基本概念。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> 如需在 SQL Server 中執行 JAVA，請參閱 [語言延伸模組文件](../language-extensions/language-extensions-overview.md)。
::: moniker-end

## <a name="what-is-machine-learning-services"></a>什麼是機器學習服務？

SQL Server 機器學習服務，可讓您在資料庫中執行 Python 和 R 指令碼。 您可以使用此服務來準備和清除資料、進行特徵工程，然後在資料庫內訓練、評估，以及部署機器學習模型。 此功能可讓您在資料所在的位置執行指令碼，而無須透過網路將資料傳輸至另一部伺服器。

機器學習服務包含了 Python 和 R 的基本發行版。 除了適用於 Python 的 [revoscalepy](python/ref-py-revoscalepy.md) 和 [microsoftml](python/ref-py-microsoftml.md)，以及適用於 R 的 [RevoScaleR](r/ref-r-revoscaler.md)、[MicrosoftML](r/ref-r-microsoftml.md)、[olapR](r/ref-r-olapr.md) 和 [sqlrutils](r/ref-r-sqlrutils.md) 這些上述 Microsoft 套件以外，您還可以安裝並使用開放原始碼套件和架構，例如 PyTorch、TensorFlow 和 scikit-learn。

機器學習服務使用擴充性架構，以在 SQL Server 中執行 Python 和 R 指令碼。 深入了解運作方式：

+ [擴充性架構](concepts/extensibility-framework.md)
+ [Python 延伸模組](concepts/extension-python.md)
+ [R 延伸模組](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>我可以使用機器學習服務來做些什麼？

您可以使用機器學習服務，在 SQL Server 內建置機器學習和深度學習模型，並加以定型。 您也可以將現有模型部署至機器學習服務，並使用關聯式資料來進行預測。

您可以使用 SQL Server 機器學習服務來進行的預測類型範例包括：

|||
|-|-|
|分類|自動將客戶意見反應分為正面與負面類別|
|迴歸/預測連續數值|根據大小和位置來預測房屋價格|
|異常偵測|偵測詐騙銀行交易 |
|建議|根據線上顧客先前的購買，來建議他們可能想要購買的產品|

### <a name="how-to-execute-python-and-r-scripts"></a>如何執行 Python 和 R 指令碼

您有兩種方式可在機器學習服務中執行 Python 和 R 指令碼。

+ 最常見的方式是使用 T-SQL 預存程序 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 您也可以使用慣用的 Python 或 R 用戶端，然後撰寫會將執行 (稱為「遠端計算內容」  ) 推送至遠端 SQL Server 的指令碼。 如需詳細資訊，請參閱設定適用於 [Python 開發](python/setup-python-client-tools-sql.md)與 [R 開發](r/set-up-a-data-science-client.md)的資料科學用戶端。

<a name="versions"></a>

## <a name="python-and-r-versions"></a>Python 和 R 版本

機器學習服務包含哪個版本的 Python 和 R，視您使用的 SQL Server 版本而定。 

| SQL Server 版本 | Python 版本 | R 版本 |
|-|-|-|
| SQL Server 2017 | 3.5.2 | 3.3.3 |
| SQL Server 2019 | 3.7.3 | 3.5.2 |

若為 SQL Server 2016 中的 R 版本，請參閱[什麼是 R 服務中的 R 版本一節](r/sql-server-r-services.md#version)

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Python 和 R 套件

除了 Microsoft 的企業套件之外，您還可以使用開放原始碼套件和架構。 最常見的開放原始碼 Python 和 R 套件都已預先安裝在機器學習服務中。 此外，也包含下列來自 Microsoft 的 Python 和 R 套件：

| Language | Package | 描述 |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | 可調整 Python 的主要套件。 資料轉換與操作、統計摘要、視覺化，以及許多模型化形式。 此外，此套件中的函式會自動在可用的核心之間分配工作負載來進行平行處理。 |
| Python | [microsoftml](python/ref-py-microsoftml.md) | 新增機器學習演算法來建立自訂模型，以進行文字分析、影像分析及情感分析。 | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | 可調整 R 的主要套件。資料轉換與操作、統計摘要、視覺化，以及許多模型化形式。 此外，此套件中的函式會自動在可用的核心之間分配工作負載來進行平行處理。 |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | 新增機器學習演算法來建立自訂模型，以進行文字分析、影像分析及情感分析。 |
| R | [olapR](r/ref-r-olapr.md) | 用於針對 SQL Server Analysis Services OLAP cube 執行 MDX 查詢的 R 函式。 |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | 一種機制，可在 T-SQL 預存程序中使用 R 指令碼、向資料庫註冊該預存程序，然後從 [R 開發環境](r/set-up-a-data-science-client.md)中執行該預存程序。 |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (MRO) 是 Microsoft 所提供的 R 加強發行版。 其為一個適用於統計分析與資料科學的完整開放原始碼平台， 並以 R 為基礎而且與其 100% 相容，且包含可提升效能和重現性的額外功能。 |

如需機器學習服務安裝了哪些套件，以及如何安裝其他套件的詳細資訊，請參閱：

+ [取得 Python 套件資訊](package-management/python-package-information.md)
+ [使用 sqlmlutils 安裝 Python 套件](package-management/install-additional-python-packages-on-sql-server.md)
+ [取得 R 套件資訊](package-management/r-package-information.md)
+ [使用 sqlmlutils 安裝新的 R 套件](package-management/install-additional-r-packages-on-sql-server.md)。

## <a name="how-do-i-get-started-with-machine-learning-services"></a>我該如何開始使用機器學習服務？

1. [安裝 SQL Server 機器學習服務](install/sql-machine-learning-services-windows-install.md)

1. 設定您的開發工具。 您可以使用：

    + [Azure Data Studio](../azure-data-studio/what-is.md) 或 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) 以使用 T-SQL 和預存程序 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 來執行您的 Python 或 R 指令碼。
    + 您自己的開發筆記型電腦或工作站上的 Python 或 R 來執行指令碼。 您可以使用 [revoscalepy](python/ref-py-revoscalepy.md) 和 [RevoScaleR](r/ref-r-revoscaler.md) 將資料提取至本機或將執行推送到遠端給 SQL Server。 如需詳細資訊，請參閱設定適用於 [Python 開發](python/setup-python-client-tools-sql.md)與 [R 開發](r/set-up-a-data-science-client.md)的資料科學用戶端。

1. 撰寫您的第一個 Python 或 R 指令碼

    + 快速入門：[執行簡單的 Python 指令碼](tutorials/quickstart-python-create-script.md)
    + 快速入門：[執行簡單的 R 指令碼](tutorials/quickstart-r-create-script.md)
    + 教學課程：[在 T-SQL 中使用 Python](tutorials/sqldev-in-database-python-for-sql-developers.md)：探索資料、執行特徵工程、訓練模型並加以部署，以及進行預測 (五部分系列)
    + 教學課程：[在 T-SQL 中使用 R](tutorials/sqldev-in-database-r-for-sql-developers.md)：探索資料、執行特徵工程、訓練模型並加以部署，以及進行預測 (五部分系列)

## <a name="next-steps"></a>後續步驟

+ [安裝 SQL Server 機器學習服務](install/sql-machine-learning-services-windows-install.md)
+ 設定適用於 [Python 開發](python/setup-python-client-tools-sql.md)與 [R 開發](r/set-up-a-data-science-client.md)的資料科學用戶端
