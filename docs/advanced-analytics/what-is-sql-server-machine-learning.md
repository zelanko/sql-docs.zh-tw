---
title: 什麼是 SQL Server Machine Learning 服務 (Python 和 R)？
titleSuffix: ''
description: Machine Learning Services 是 SQL Server 中的一項功能, 可讓您以關聯式資料執行 Python 和 R 腳本。 您可以使用開放原始碼套件和架構, 以及適用于預測性分析和機器學習的 Microsoft Python 和 R 套件。 腳本會在資料庫中執行, 而不會將資料移出 SQL Server 或透過網路。 本文說明 SQL Server Machine Learning 服務的基本概念。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/07/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 59e005e0075c9bb26210c6be9be5f52a3aa9a164
ms.sourcegitcommit: 3ec48823bee1c092ce2aba6011b95174de03fb65
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926917"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>什麼是 SQL Server Machine Learning 服務 (Python 和 R)？
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services 是 SQL Server 中的一項功能, 可讓您以關聯式資料執行 Python 和 R 腳本。 您可以使用開放原始碼套件和架構, 以及適用于預測性分析和機器學習的[Microsoft Python 和 R 套件](#packages)。 腳本會在資料庫中執行, 而不會將資料移出 SQL Server 或透過網路。 本文說明 SQL Server Machine Learning 服務的基本概念。

在 Azure SQL Database 中, [Machine Learning 服務](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview)目前為公開預覽狀態。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> 如需在 SQL Server 中執行 JAVA, 請參閱[語言延伸模組檔](../language-extensions/language-extensions-overview.md)。
::: moniker-end

## <a name="what-is-machine-learning-services"></a>什麼是 Machine Learning 服務？

SQL Server Machine Learning 服務可讓您在資料庫內執行 Python 和 R 腳本。 您可以使用它來準備和清除資料、進行功能工程設計, 以及在資料庫中定型、評估和部署機器學習模型。 此功能會在資料所在的位置執行您的腳本, 並消除透過網路傳送資料到另一部伺服器的情況。

Python 和 R 的基底散發套件包含在 Machine Learning 服務中。 除了適用于 Python 的 Microsoft 套件[revoscalepy](python/ref-py-revoscalepy.md)和[Microsoftml](python/ref-py-microsoftml.md) , 以及[RevoScaleR](r/ref-r-revoscaler.md)、 [microsoftml](r/ref-r-microsoftml.md)、 [olapR](r/ref-r-olapr.md)之外, 您還可以使用開放原始碼套件和架構, 例如 PyTorch、TensorFlow 和 scikit-learn 學習。和適用于 R 的[sqlrutils](r/ref-r-sqlrutils.md) 。

Machine Learning Services 會使用擴充性架構, 在 SQL Server 中執行 Python 和 R 腳本。 深入瞭解其運作方式:

+ [擴充性架構](concepts/extensibility-framework.md)
+ [Python 延伸模組](concepts/extension-python.md)
+ [R 擴充功能](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>我可以使用 Machine Learning 服務來做些什麼？

您可以使用 Machine Learning 服務, 在 SQL Server 內建立和定型機器學習和深度學習模型。 您也可以將現有的模型部署到 Machine Learning 服務, 並使用關聯式資料進行預測。

您可以 SQL Server Machine Learning 服務使用的預測類型範例包括:

|||
|-|-|
|分類/分類|自動將客戶意見分割成正面和負面的類別|
|回歸/預測連續值|根據大小和位置來預測房屋價格|
|異常偵測|偵測詐騙銀行交易 |
|建議|根據先前的購買專案, 建議線上購物者可能想要購買的產品|

### <a name="how-to-execute-python-and-r-scripts"></a>如何執行 Python 和 R 腳本

有兩種方式可以在 Machine Learning 服務中執行 Python 和 R 腳本:

+ 最常見的方式是使用 T-sql 預存程式[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 您也可以使用慣用的 Python 或 R 用戶端, 並撰寫將執行 (稱為*遠端計算內容*) 推送至遠端 SQL Server 的腳本。 如需詳細資訊, 請參閱如何針對[Python 開發](python/setup-python-client-tools-sql.md)和[R 開發](r/set-up-a-data-science-client.md)設定資料科學用戶端。

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Python 和 R 套件

除了 Microsoft 的企業套件以外, 您還可以使用開放原始碼套件和架構。 最常見的開放原始碼 Python 和 R 套件都已預先安裝在 Machine Learning 服務中。 Microsoft 的下列 Python 和 R 套件也包含在內:

| 語言 | 套件 | 描述 |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | 可擴充 Python 的主要套件。 資料轉換和操作、統計摘要、視覺效果, 以及許多形式的模型化。 此外, 此套件中的函式會自動將工作負載分散到可用的核心, 以進行平行處理。 |
| Python | [microsoftml](python/ref-py-microsoftml.md) | 新增機器學習演算法, 以建立文字分析、影像分析和情感分析的自訂模型。 | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | 可調整 R 的主要套件。資料轉換和操作、統計摘要、視覺效果, 以及許多形式的模型化。 此外, 此套件中的函式會自動將工作負載分散到可用的核心, 以進行平行處理。 |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | 新增機器學習演算法, 以建立文字分析、影像分析和情感分析的自訂模型。 |
| R | [olapR](r/ref-r-olapr.md) | 用於對 SQL Server Analysis Services OLAP Cube 進行 MDX 查詢的 R 函數。 |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | 在 T-sql 預存程式中使用 R 腳本的機制、向資料庫註冊該預存程式, 以及從[R 開發環境](r/set-up-a-data-science-client.md)執行預存程式。 |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open (MRO) 是由 Microsoft 加強的 R 散發。 這是適用于統計分析和資料科學的完整開放原始碼平臺。 它是以與 R 相容的 100% 為基礎, 並包含改善效能和重現性的其他功能。 |

## <a name="how-do-i-get-started-with-machine-learning-services"></a>如何? 開始使用 Machine Learning 服務？

1. [安裝 SQL Server Machine Learning 服務](install/sql-machine-learning-services-windows-install.md)

1. 設定您的開發工具。 您可以使用:

    + [Azure Data Studio](../azure-data-studio/what-is.md)或[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) , 以使用 t-sql 和預存程式[Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)來執行您的 Python 或 R 腳本。
    + 在您自己的開發膝上型電腦或工作站上的 Python 或 R 來執行腳本。 您可以在本機提取資料, 或使用[revoscalepy](python/ref-py-revoscalepy.md)和[RevoScaleR](r/ref-r-revoscaler.md)從遠端將執行推送至 SQL Server。 如需詳細資訊, 請參閱如何針對[Python 開發](python/setup-python-client-tools-sql.md)和[R 開發](r/set-up-a-data-science-client.md)設定資料科學用戶端。

1. 撰寫您的第一個 Python 或 R 腳本

    + 快速入門：[在 Python](tutorials/quickstart-python-run-using-t-sql.md)或[R 中](tutorials/quickstart-r-run-using-tsql.md)執行 "Hello world" 腳本
    + 快速入門：[在 Python](tutorials/quickstart-python-train-score-in-tsql.md)或[R 中](tutorials/quickstart-r-create-predictive-model.md)建立預測模型
    + 教學課程：[在 t-sql 中使用 Python](tutorials/sqldev-in-database-python-for-sql-developers.md):探索資料、執行特徵工程設計、定型和部署模型, 以及進行預測 (五個部分的系列)
    + 教學課程：[在 t-sql 中使用 R](tutorials/sqldev-in-database-r-for-sql-developers.md):探索資料、執行特徵工程設計、定型和部署模型, 以及進行預測 (五個部分的系列)
    + 教學課程：[使用 R 工具中的 Machine Learning 服務](tutorials/walkthrough-data-science-end-to-end-walkthrough.md):流覽資料、建立圖形和繪圖、執行特徵工程設計、定型和部署模型, 以及進行預測 (六個部分的系列)

## <a name="next-steps"></a>後續步驟

+ [安裝 SQL Server Machine Learning 服務](install/sql-machine-learning-services-windows-install.md)
+ 設定適用于[Python 開發](python/setup-python-client-tools-sql.md)和[R 開發](r/set-up-a-data-science-client.md)的資料科學用戶端
