---
title: Python 教學課程
titleSuffix: SQL machine learning
description: 本文說明 SQL 機器學習的 Python 教學課程。 了解如何執行指令碼及建置機器學習模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: f417a92a00b290f06326433b24b73137a0a424fa
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178545"
---
# <a name="python-tutorials-for-sql-machine-learning"></a>SQL 機器學習的 Python 教學課程
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
本文說明 [SQL Server](../sql-server-machine-learning-services.md) 和[巨量資料叢集](../../big-data-cluster/machine-learning-services.md)上機器學習服務的 Python 教學課程和快速入門。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
本文說明 [SQL Server 機器學習服務](../sql-server-machine-learning-services.md)的 Python 教學課程和快速入門。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
本文描述 [Azure SQL 受控執行個體機器學習服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)的 Python 教學課程和快速入門。
::: moniker-end

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Python 教學課程

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
| 教學課程 | 描述 |
|-|-|
| [使用線性迴歸來預測雪橇租賃](python-ski-rental-linear-regression.md) | 使用 Python 和線性迴歸來預測雪橇租賃的數量。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
| [使用 k-means 叢集將客戶分類](python-clustering-model.md) | 使用 Python 來開發及部署 K-Means 叢集模型，以將客戶分類。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
| [使用 revoscalepy 建立模型](use-python-revoscalepy-to-create-model.md) | 示範如何使用 SQL Server 作為計算內容，從遠端 Python 用戶端執行程式碼。 本教學課程會從 **revoscalepy** 程式庫使用 **rxLinMod** 建立模型。 |
| [適用於 SQL 開發人員的 Python 資料分析](python-taxi-classification-introduction.md) | 此端對端逐步解說示範使用 T-SQL 建立完整 Python 解決方案的處理序。 |
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
| 教學課程 | 描述 |
|-|-|
| [使用線性迴歸來預測雪橇租賃](python-ski-rental-linear-regression.md) | 使用 Python 和線性迴歸來預測雪橇租賃的數量。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
| [使用 k-means 叢集將客戶分類](python-clustering-model.md) | 使用 Python 來開發及部署 K-Means 叢集模型，以將客戶分類。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
::: moniker-end

## <a name="python-quickstarts"></a>Python 快速入門

如果您不熟悉 SQL 機器學習，也可以嘗試 Python 快速入門。

| 快速入門 | 描述 |
|-|-|
| [執行簡單的 Python 指令碼](quickstart-python-create-script.md) | 了解如何使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，在 T-SQL 中呼叫 Python 的基本概念。 |
| [使用 Python 的資料結構與物件](quickstart-python-data-structures.md) | 顯示 SQL 如何使用 Python Pandas 套件來處理資料結構。 |
| [在 Python 中建立預測模型並為其評分](quickstart-python-train-score-model.md) | 說明如何建立、訓練及使用 Python 模型，以從新的資料進行預測。 |

## <a name="next-steps"></a>後續步驟

+ [SQL Server 中的 Python 延伸模組](../concepts/extension-python.md)
