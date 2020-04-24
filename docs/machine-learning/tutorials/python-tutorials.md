---
title: Python 教學課程
description: 此文章描述 SQL Server 機器學習服務的 Python 教學課程。 了解如何在 SQL Server 中執行指令碼及建置機器學習模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e3733f12ed93d7c84a86259742b6996333c3900f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487348"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的 Python 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明 [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)的 Python 教學課程和快速入門。

+ 了解如何執行 Python 指令碼。
+ 建置、訓練 Python 模型，並部署至 SQL Server。
+ 了解遠端和本機計算內容。
+ 探索適用於資料科學和機器學習的 Microsoft Python 套件。

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Python 教學課程

| 教學課程 | 描述 |
|-|-|
| [使用線性迴歸來預測雪橇租賃](python-ski-rental-linear-regression.md) | 使用 Python 和線性迴歸來預測雪橇租賃的數量。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
| [使用 k-means 叢集將客戶分類](python-clustering-model.md) | 使用 Python 來開發及部署 K-Means 叢集模型，以將客戶分類。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
| [使用 revoscalepy 建立模型](use-python-revoscalepy-to-create-model.md) | 示範如何使用 SQL Server 作為計算內容，從遠端 Python 用戶端執行程式碼。 本教學課程會從 **revoscalepy** 程式庫使用 **rxLinMod** 建立模型。 |
| [適用於 SQL 開發人員的 Python 資料分析](sqldev-in-database-python-for-sql-developers.md) | 此端對端逐步解說示範使用 T-SQL 建立完整 Python 解決方案的處理序。 |

## <a name="python-quickstarts"></a>Python 快速入門

如果您不熟悉 SQL Server 機器學習服務，也可以嘗試 Python 快速入門。

| 快速入門 | 描述 |
|-|-|
| [Python 和 SQL Server 中的 Hello World](quickstart-python-create-script.md) | 了解如何使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，在 T-SQL 中呼叫 Python 的基本概念。 |
| [在 SQL Server 中使用 Python 處理資料類型和物件](quickstart-python-data-structures.md) | 顯示 SQL Server 如何使用 Python Pandas 套件來處理資料結構。 |
| [在 Python 中建立預測模型並為其評分](quickstart-python-train-score-model.md) | 說明如何建立、訓練及使用 Python 模型，以從新的資料進行預測。 |

## <a name="next-steps"></a>後續步驟

+ [什麼是 SQL Server 機器學習服務 (Python 和 R)？](../sql-server-machine-learning-services.md)
+ [SQL Server 的 Python 延伸模組](../concepts/extension-python.md)