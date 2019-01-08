---
title: SQL Server 的 R 教學課程概觀-SQL Server Machine Learning
description: SQL Server 資料庫內分析的 R 語言教學課程簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4353d50ecfd8aac3ada1c71baf1be78f13c51b11
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596529"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server R 語言教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明在資料庫內分析的 R 語言教學課程[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)或是[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)。

+ 了解如何自動換行及預存程序中執行 R 程式碼。
+ 序列化，並將 r 為基礎的模型儲存至 SQL Server 資料庫。
+ 深入了解遠端和本機計算內容，以及何時使用它們。
+ 探索資料科學與機器學習工作的 Microsoft R 程式庫。

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R 快速入門和教學課程

| 連結 | 描述 |
|------|-------------|
| [快速入門：在 T-SQL 中使用 R](rtsql-using-r-code-in-transact-sql-quickstart.md) | 與這個說明呼叫使用 T-SQL 查詢編輯器，例如 SQL Server Management Studio 的 R 函數的基本語法的幾個快速入門的第一個。 |
| [教學課程：了解適用於資料科學家的資料庫內 R 分析](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | 適用於 SQL server 的 R 開發人員，本教學課程說明如何請執行一般資料科學工作在 SQL Server。 載入和視覺化資料、 定型和模型儲存至 SQL Server，和使用模型進行預測性分析。 |
| [教學課程：了解適用於 SQL 開發人員的資料庫內 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md) | 建置和部署完整的 R 解決方案，只使用[!INCLUDE[tsql](../../includes/tsql-md.md)]工具。 著重於將方案移到生產環境。 您將了解如何將 R 程式碼包裝在預存程序中、將 R 模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，以及對 R 模型進行參數化呼叫來進行預測。 |
| [教學課程：RevoScalepR 深入探討](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | 了解如何使用 RevoScaleR 套件中的函數。 R 與 SQL Server 及交換器之間移動資料計算內容以符合特定的工作。 建立模型和繪圖，和您的開發環境和資料庫伺服器之間移動它們。 |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>程式碼範例

| 連結 | 描述 |
|------|-------------|
| [使用 R 和 SQL Server 的預測性模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 了解如何使用 ski 租賃業務的機器學習服務預測未來，它可以幫助商務計劃和人員滿足未來需求。 |
| [執行客戶使用 R 和 SQL Server 叢集](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 使用非監督式的學習來區分客戶的銷售資料為基礎。 |

## <a name="see-also"></a>另請參閱

+ [SQL server 的 R 延伸模組](../concepts/extension-r.md)
+ [SQL Server 機器學習服務教學課程](machine-learning-services-tutorials.md)

