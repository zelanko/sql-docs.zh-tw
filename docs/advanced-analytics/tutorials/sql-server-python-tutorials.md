---
title: SQL Server 2017 Python 教學課程概觀-SQL Server Machine Learning
description: SQL Server 2017 資料庫內分析的 Python 教學課程簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: d5a434b6e089cd77a2bd685506e5552c4e1e7f6d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961942"
---
# <a name="sql-server-2017-python-tutorials"></a>SQL Server 2017 Python 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明在資料庫內分析的 Python 教學課程[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)。 

+ 了解如何自動換行及預存程序中執行 Python 程式碼。
+ 序列化，並將 Python 為基礎的模型儲存至 SQL Server 資料庫。
+ 深入了解遠端和本機計算內容，以及何時使用它們。
+ 探索 Microsoft Python 模組，用於資料科學和機器學習工作。

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Python 快速入門和教學課程

| 連結 | 描述 |
|------|-------------|
| [快速入門：SQL Server 中的"Hello world"Python 指令碼](quickstart-python-run-using-t-sql.md) | 了解如何在 T-SQL 中呼叫 Python 的基本概念。 |
| [快速入門：建立、 定型和使用 SQL Server 中的預存程序中的 Python 模型](quickstart-python-train-score-in-tsql.md) | 說明將 Python 程式碼內嵌在預存程序，提供輸入和預存程序執行的機制。 |
| [教學課程：使用 revoscalepy 建立模型](use-python-revoscalepy-to-create-model.md) | 示範如何從遠端 Python 終端機中，使用 SQL Server 計算內容中執行程式碼。 您應該略為熟悉 Python 工具和環境。 範例程式碼是提供來建立模型，使用**rxLinMod**，從新**revoscalepy**程式庫。 |
| [教學課程：了解適用於 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md) | 此端對端逐步解說示範如何建置完整的 Python 解決方案，使用 T-SQL 預存程序的程序。 包含所有 Python 程式碼都。|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>程式碼範例

這些範例和 SQL Server 開發團隊所提供的示範反白顯示您可以在真實世界應用程式中使用內嵌的分析方式。

| 連結 | 描述 |
|------|-------------|
| [使用 Python 和 SQL Server 的預測性模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 了解如何使用 ski 租賃業務的機器學習服務預測未來，它可以幫助商務計劃和人員滿足未來需求。 |
| [執行客戶使用 Python 和 SQL Server 叢集](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 了解如何使用 Kmeans 演算法來執行非監督式叢集的客戶。 |

## <a name="see-also"></a>另請參閱

+ [SQL server 的 Python 擴充功能](../concepts/extension-python.md)
+ [SQL Server 機器學習服務教學課程](machine-learning-services-tutorials.md)
