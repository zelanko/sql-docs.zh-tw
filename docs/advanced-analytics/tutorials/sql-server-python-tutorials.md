---
title: SQL Server 2017 Python 教學課程總覽
description: SQL Server 2017 資料庫內分析的 Python 教學課程簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 65dd2197d9fb079da116908871d931ad19370cf5
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714774"
---
# <a name="sql-server-2017-python-tutorials"></a>SQL Server 2017 Python 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)上的資料庫內分析的 Python 教學課程。 

+ 瞭解如何在預存程式中包裝和執行 Python 程式碼。
+ 將以 Python 為基礎的模型序列化並儲存至 SQL Server 資料庫。
+ 瞭解遠端和本機計算內容, 以及使用它們的時機。
+ 探索適用于資料科學和機器學習工作的 Microsoft Python 模組。

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Python 快速入門與教學課程

| 連結 | 描述 |
|------|-------------|
| [入門SQL Server 中的 "Hello world" Python 腳本](quickstart-python-run-using-t-sql.md) | 瞭解如何在 T-sql 中呼叫 Python 的基本概念。 |
| [入門在 SQL Server 中使用預存程式來建立、定型和使用 Python 模型](quickstart-python-train-score-in-tsql.md) | 說明在預存程式中內嵌 Python 程式碼、提供輸入和預存程式執行的機制。 |
| [教學課程：使用 revoscalepy 建立模型](use-python-revoscalepy-to-create-model.md) | 示範如何使用 SQL Server 計算內容, 從遠端 Python 終端機執行程式碼。 您應該有點熟悉 Python 工具和環境。 提供的範例程式碼會使用**rxLinMod**從新的**revoscalepy**程式庫建立模型。 |
| [教學課程：瞭解適用于 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md) | 此端對端逐步解說示範使用 T-sql 預存程式建立完整 Python 解決方案的流程。 包含所有 Python 程式碼。|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>程式碼範例

SQL Server 開發小組所提供的這些範例和示範, 會醒目提示您可以在真實世界應用程式中使用內嵌分析的方式。

| 連結 | 描述 |
|------|-------------|
| [使用 Python 和 SQL Server 建立預測模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 瞭解 ski 出租公司如何使用機器學習來預測未來的租用, 以協助商務計畫和員工滿足未來的需求。 |
| [使用 Python 和 SQL Server 執行客戶叢集](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | 瞭解如何使用 Kmeans 演算法來執行客戶的不受監督叢集。 |

## <a name="see-also"></a>另請參閱

+ [SQL Server 的 Python 延伸模組](../concepts/extension-python.md)
+ [SQL Server Machine Learning Services 教學課程](machine-learning-services-tutorials.md)
