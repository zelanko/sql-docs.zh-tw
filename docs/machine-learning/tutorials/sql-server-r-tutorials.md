---
title: R 教學課程
description: SQL Server 資料庫內分析的 R 語言教學課程簡介。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 62264f728fec5b68c3034fb3c6260f04617353b5
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116111"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server R 語言教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 或 [SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md)中，資料庫內分析的 R 語言教學課程。

+ 了解如何在預存程序中包裝和執行 R 程式碼。
+ 序列化以 R 為基礎的模型，並將其儲存至 SQL Server 資料庫。
+ 了解遠端和本機計算內容，以及使用時機。
+ 探索適用於資料科學和機器學習工作的 Microsoft R 程式庫。

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R 快速入門與教學課程

| 連結 | 描述 |
|------|-------------|
| [快速入門：建立及執行簡易的 R 指令碼](quickstart-r-create-script.md) | 在多項快速入門中，首先說明使用 T-SQL 查詢編輯器 (例如 SQL Server Management Studio) 呼叫 R 函數的基本語法。 |
| [教學課程：了解適用於資料科學家的資料庫內 R 分析](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | 本教學課程為剛接觸 SQL Server 的 R 開發人員說明如何在 SQL Server 中執行常見的資料科學工作。 載入資料並將其視覺化、將模型定型並儲存至 SQL Server，並使用模型進行預測性分析。 |
| [教學課程：了解適用於 SQL 開發人員的資料庫內 R 分析](../tutorials/sqldev-in-database-r-for-sql-developers.md) | 僅使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 工具來建置和部署完整的 R 解決方案。 著重於將解決方案移至生產環境。 您將了解如何將 R 程式碼包裝在預存程序中、將 R 模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，以及對 R 模型進行參數化呼叫來進行預測。 |
| [教學課程：RevoScaleR 深入探討](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | 了解如何使用 RevoScaleR 套件中的函數。 在 R 與 SQL Server 之間移動資料，並切換計算內容以符合特定的工作。 建立模型和繪圖，並在您的開發環境和資料庫伺服器之間移動兩者。 |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>程式碼範例

| 連結 | 描述 |
|------|-------------|
| [使用 R 和 SQL Server 建置預測模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 了解滑雪板租賃業如何使用機器學習服務預測未來的租賃業務，這有助於商務方案和人員滿足未來的需求。 |
| [使用 R 和 SQL Server 執行客戶叢集](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 根據銷售資料使用無人監督的學習來區隔客戶。 |

## <a name="see-also"></a>另請參閱

+ [SQL Server 的 R 延伸模組](../concepts/extension-r.md)