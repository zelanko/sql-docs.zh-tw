---
title: R 教學課程
titleSuffix: SQL machine learning
description: 本文說明 SQL 機器學習的 R 教學課程。 了解如何執行指令碼及建置機器學習模型。
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/21/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: ac7bbbb10d736b68d3e9930fafd7ae6e50f739f0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85671023"
---
# <a name="r-tutorials-for-sql-machine-learning"></a>SQL 機器學習的 R 教學課程
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
本文說明 [SQL Server](../sql-server-machine-learning-services.md) 和[巨量資料叢集](../../big-data-cluster/machine-learning-services.md)上機器學習服務的 R 教學課程和快速入門。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
此文章說明 [SQL Server 機器學習服務](../sql-server-machine-learning-services.md)的 R 教學課程和快速入門。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
此文說明 [SQL Server 2016 R Services](../r/sql-server-r-services.md) 的 R 教學課程和快速入門。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
本文描述 [Azure SQL 受控執行個體機器學習服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)的 Python 教學課程和快速入門。
::: moniker-end

<a name="bkmk_sqltutorials"></a>

## <a name="r-tutorials"></a>R 教學課程

::: moniker range=">=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions"
| 教學課程 | 描述 |
|------|-------------|
| [使用決策樹預測滑雪工具租用](r-predictive-model-introduction.md) | 使用 R 和決策樹模型來預測未來的滑雪工具租用數。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
| [使用 k-means 叢集將客戶分類](r-clustering-model-introduction.md) | 使用 R 來開發及部署 K-Means 群集模型，以將客戶分類。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
| [適用於資料科學家的資料庫內 R 分析](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | 本教學課程為剛接觸 SQL 機器學習的 R 開發人員說明如何在 SQL 中執行常見資料科學工作。 載入資料並將其視覺化、將模型定型並儲存在資料庫中，以及使用模型進行預測性分析。 |
| [適用於 SQL 開發人員的資料庫內 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md) | 僅使用 SQL 工具來建置和部署完整的 R 解決方案。 著重於將解決方案移至生產環境。 您將了解如何將 R 程式碼包裝在預存程序中、將 R 模型儲存在資料庫中，以及對 R 模型進行參數化呼叫來進行預測。 |
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
| 教學課程 | 描述 |
|------|-------------|
| [使用決策樹預測滑雪工具租用](r-predictive-model-introduction.md) | 使用 R 和決策樹模型來預測未來的滑雪工具租用數。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
| [使用 k-means 叢集將客戶分類](r-clustering-model-introduction.md) | 使用 R 來開發及部署 K-Means 群集模型，以將客戶分類。 在 Azure Data Studio 中使用筆記本來準備資料及訓練模型，並使用 T-SQL 進行模型部署。 |
::: moniker-end

## <a name="r-quickstarts"></a>R 快速入門

如果您不熟悉 SQL 機器學習，也可以嘗試 R 快速入門。

| 快速入門 | 描述 |
|-|-|
| [執行簡單的 R 指令碼](quickstart-r-create-script.md) | 了解如何使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，在 T-SQL 中呼叫 R 的基本概念。 |
| [使用 R 的資料結構與物件](quickstart-r-data-types-and-objects.md) | 顯示 SQL 如何使用 R 來處理資料結構。 |
| [在 R 中建立預測模型並為其評分](quickstart-r-data-types-and-objects.md) | 說明如何建立、訓練及使用 R 模型，以從新的資料進行預測。 |

## <a name="next-steps"></a>後續步驟

+ [SQL Server 中的 Python 延伸模組](../concepts/extension-r.md)
