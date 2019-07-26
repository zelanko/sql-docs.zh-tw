---
title: SQL Server R 教學課程總覽
description: SQL Server 資料庫內分析的 R 語言教學課程簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: cd03837644ec1cd4d818615bb8a17728c58a1f17
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470589"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server R 語言教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明在[SQL Server 2016 R 服務](../install/sql-r-services-windows-install.md)或[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)上進行資料庫內分析的 R 語言教學課程。

+ 瞭解如何在預存程式中包裝和執行 R 程式碼。
+ 序列化以 r 為基礎的模型, 並將其儲存至 SQL Server 資料庫。
+ 瞭解遠端和本機計算內容, 以及使用它們的時機。
+ 探索適用于資料科學和機器學習工作的 Microsoft R 程式庫。

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R 快速入門與教學課程

| 連結 | 描述 |
|------|-------------|
| [入門在 T-sql 中使用 R](rtsql-using-r-code-in-transact-sql-quickstart.md) | 首先是幾個快速入門, 其中說明使用 T-SQL 查詢編輯器 (例如 SQL Server Management Studio) 呼叫 R 函數的基本語法。 |
| [教學課程：瞭解適用于資料科學家的資料庫內 R 分析](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | 針對 SQL Server 的新手開發人員, 本教學課程說明如何在 SQL Server 中執行常見的資料科學工作。 載入資料並將其視覺化、將模型定型並儲存至 SQL Server, 並使用模型進行預測性分析。 |
| [教學課程：瞭解適用于 SQL 開發人員的資料庫內 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md) | 使用[!INCLUDE[tsql](../../includes/tsql-md.md)]工具來建立和部署完整的 R 解決方案。 著重于將解決方案移至生產環境。 您將了解如何將 R 程式碼包裝在預存程序中、將 R 模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，以及對 R 模型進行參數化呼叫來進行預測。 |
| [教學課程：RevoScalepR 深入探討](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | 瞭解如何使用 RevoScaleR 套件中的函數。 在 R 與 SQL Server 之間移動資料, 並切換計算內容以符合特定工作。 建立模型和繪圖, 並在您的開發環境和資料庫伺服器之間移動它們。 |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>程式碼範例

| 連結 | 描述 |
|------|-------------|
| [使用 R 和 SQL Server 建立預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 瞭解 ski 出租公司如何使用機器學習來預測未來的租用, 以協助商務計畫和員工滿足未來的需求。 |
| [使用 R 和 SQL Server 執行客戶群集](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用不受監督 learning 根據銷售資料來分割客戶。 |

## <a name="see-also"></a>另請參閱

+ [SQL Server 的 R 擴充功能](../concepts/extension-r.md)
+ [SQL Server Machine Learning Services 教學課程](machine-learning-services-tutorials.md)

