---
title: Python 教學課程
description: 本文說明 SQL Server Machine Learning 服務的 Python 教學課程。 瞭解如何執行 Python 腳本。 建立、定型和部署 Python 模型以 SQL Server。 瞭解遠端和本機計算內容。 探索適用于資料科學和機器學習的 Microsoft Python 套件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 80f714810acd8c04c80fe0b8abe5214a456f6dd6
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199404"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>適用于 SQL Server Machine Learning 服務的 Python 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明[SQL Server Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)的 Python 教學課程和快速入門。

+ 瞭解如何執行 Python 腳本。
+ 建立、定型和部署 Python 模型以 SQL Server。
+ 瞭解遠端和本機計算內容。
+ 探索適用于資料科學和機器學習的 Microsoft Python 套件。

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Python 教學課程

| 教學課程 | 描述 |
|-|-|
| [使用線性回歸來預測 ski 出租](python-ski-rental-linear-regression.md) | 使用 Python 和線性回歸來預測 ski 租用的數目。 在 Azure Data Studio 中使用筆記本來準備資料和定型模型，以及用於部署模型的 T-sql。 |
| [使用 k--表示叢集分類客戶](python-clustering-model.md) | 使用 Python 來開發和部署 K 意指的叢集模型，以將客戶分類。 在 Azure Data Studio 中使用筆記本來準備資料和定型模型，以及用於部署模型的 T-sql。 |
| [使用 revoscalepy 建立模型](use-python-revoscalepy-to-create-model.md) | 示範如何使用 SQL Server 作為計算內容，從遠端 Python 用戶端執行程式碼。 本教學課程會使用**revoscalepy**程式庫中的**rxLinMod**來建立模型。 |
| [適用于 SQL 開發人員的 Python 資料分析](sqldev-in-database-python-for-sql-developers.md) | 此端對端逐步解說示範使用 T-sql 建立完整 Python 解決方案的程式。 |

## <a name="python-quickstarts"></a>Python 快速入門

如果您不熟悉 SQL Server Machine Learning 服務，您也可以嘗試 Python 快速入門。

| 快速入門 | 描述 |
|-|-|
| [Python 和 SQL Server 中的 Hello World](quickstart-python-create-script.md) | 瞭解如何使用[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)在 t-sql 中呼叫 Python 的基本概念。 |
| [在 SQL Server 中使用 Python 處理資料類型和物件](quickstart-python-data-structures.md) | 顯示 SQL Server 如何使用 Python pandas 封裝來處理資料結構。 |
| [在 Python 中建立預測模型並為其評分](quickstart-python-train-score-model.md) | 說明如何建立、定型和使用 Python 模型，以從新的資料進行預測。 |

## <a name="next-steps"></a>後續步驟

+ [什麼是 SQL Server Machine Learning 服務（Python 和 R）？](../what-is-sql-server-machine-learning.md)
+ [SQL Server 的 Python 延伸模組](../concepts/extension-python.md)