---
title: SQL Server Python 教學課程 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5cafb253cea118148bd654ea770234843f742838
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2018
ms.locfileid: "49383333"
---
# <a name="sql-server-python-tutorials"></a>SQL Server Python 教學課程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供一份教學課程和範例，示範如何使用 Python 與 SQL Server 2017。 透過這些範例和示範，您將了解：

+ 如何從 T-SQL 執行 Python
+ 遠端和本機計算內容，和如何執行 Python 程式碼使用 SQL Server 電腦有哪些？
+ 如何將 Python 程式碼包裝在預存程序
+ 最佳化 SQL 生產環境中的 Python 程式碼
+ 內嵌在應用程式中的機器學習服務的真實世界案例

如需需求和安裝資訊，請參閱[必要條件](#bkmk_Prerequisites)。

## <a name="bkmk_pythontutorials"></a>Python 教學課程

+ [在 T-SQL 中執行 Python](run-python-using-t-sql.md)

   了解如何使用 T-SQL 和，於 SQL Server 2016 的擴充性機制中呼叫 Python 的基本概念。

+ [建立機器學習中使用 revoscalepy Python 模型](use-python-revoscalepy-to-create-model.md)

   這一課會示範如何執行程式碼從遠端的 Python 終端機中，使用 SQL Server 計算內容。 您應該略為熟悉 Python 工具和環境。 範例程式碼是提供來建立模型，使用**rxLinMod**，從新**revoscalepy**程式庫。 

+ [適用於 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)

    此端對端逐步解說示範如何建置完整的 Python 解決方案，使用 T-SQL 預存程序的程序。 包含所有 Python 程式碼都。


## <a name="python-samples"></a>Python 範例

這些範例和 SQL Server 開發團隊所提供的示範反白顯示您可以在真實世界應用程式中使用內嵌的分析方式。

+ [使用 Python 和 SQL Server 的預測性模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  了解如何使用 ski 租賃業務的機器學習服務預測未來，它可以幫助商務計劃和人員滿足未來需求。

  > [!TIP]
  > 現在包含原生評分，從 Python 模型 ！

+ [執行客戶使用 Python 和 SQL Server 叢集](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    了解如何使用 Kmeans 演算法來執行非監督式叢集的客戶。

## <a name="see-also"></a>另請參閱

[適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)
