---
title: R 與 Python 機器學習及程式設計延伸模組文件 - SQL Server 機器學習服務
description: SQL Server 中的 R 和 Python，內建資料科學模型和機器學習服務演算法，可大規模地進行企業資料分析。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/10/2019
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 61d7d969e4ec51914e2467895b5e8b9bc2e00f06
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/25/2019
ms.locfileid: "56803449"
---
# <a name="sql-server-machine-learning"></a>SQL Server 機器學習服務

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"

## <a name="sql-server-machine-learning-and-programming-extensions-documentation"></a>SQL Server 機器學習服務與程式設計延伸模組文件

使用我們的快速入門、教學課程和操作說明文章，了解如何在常駐的關聯式資料上使用 R 和 Python 外部程式庫和語言。 [SQL Server 機器學習服務](what-is-sql-server-machine-learning.md)中的 R 和 Python 程式庫包含基本發佈、資料科學模型、機器學習服務演算法，以及可大規模地進行高效能分析的函式，而不需要在網路之間傳輸資料。

在 SQL Server 2019 中，Java 程式碼執行使用與 R 和 Python 相同的擴充性架構，但不包含資料科學與機器學習服務函數庫。 如需新功能的詳細資訊，請參閱 [SQL Server 機器學習服務的新功能](what-s-new-in-sql-server-machine-learning-services.md)。

|   |   |
|---|:--|
| ![R 標誌](media/index/logo_r.png) | 開放原始碼 R，以 [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) 和 [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) 中的 Microsoft AI 演算法擴充。 這些程式庫提供您預估和預測模型、統計分析、視覺效果，並可大規模地進行資料操作。<br/>R 整合從 [SQL Server 2016](install/sql-r-services-windows-install.md) 開始，而且 [SQL Server 2017](install/sql-machine-learning-services-windows-install.md) 中也有提供。 |
| ![Python 標誌](media/index/logo_python.png) | Python 開發人員可以使用 Microsoft [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 和 [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) 程式庫大規模地執行預測性分析和機器學習服務。 Anaconda 和 Python 3.5 相容程式庫是基本發佈。<br/>Python 整合從 [SQL Server 2017](install/sql-machine-learning-services-windows-install.md) 開始。 |
| ![Java 標誌](media/index/logo_java.png) | Java 開發人員可以使用 [Java 語言延伸模組](java/extension-java.md)，將程式碼包裝成預存程序或可透過 Transact-SQL 存取的二進位格式。<br/>Java 整合從 [SQL Server 2019 (預覽)](install/sql-machine-learning-services-ver15.md) 開始。 |
| &nbsp; | &nbsp; |
::: moniker-end

::: moniker range="=sql-server-2016||=sql-server-2017"

## <a name="sql-server-machine-learning-r-and-python-documentation"></a>SQL Server 機器學習服務 R 和 Python 文件

使用我們的快速入門、教學課程和操作說明文章，了解如何在常駐的關聯式資料上使用 R 和 Python 外部程式庫和語言。 [SQL Server 機器學習服務](what-is-sql-server-machine-learning.md)中的 R 和 Python 程式庫包含基本發佈、資料科學模型、機器學習服務演算法，以及可大規模地進行高效能分析的函式，而不需要在網路之間傳輸資料。

|   |   |
|---|:--|
| ![R 標誌](media/index/logo_r.png) | 開放原始碼 R，以 [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) 和 [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) 中的 Microsoft AI 演算法擴充。 這些程式庫提供您預估和預測模型、統計分析、視覺效果，並可大規模地進行資料操作。<br/>R 整合從 [SQL Server 2016](install/sql-r-services-windows-install.md) 開始，而且 [SQL Server 2017](install/sql-machine-learning-services-windows-install.md) 中也有提供。 |
| ![Python 標誌](media/index/logo_python.png) | Python 開發人員可以使用 Microsoft [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 和 [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) 程式庫大規模地執行預測性分析和機器學習服務。 Anaconda 和 Python 3.5 相容程式庫是基本發佈。<br/>Python 整合從 [SQL Server 2017](install/sql-machine-learning-services-windows-install.md) 開始。 |
| &nbsp; | &nbsp; |
::: moniker-end

## <a name="5-minute-quickstarts"></a>5 分鐘快速入門

- [在 R 中建立預測模型](tutorials/rtsql-create-a-predictive-model-r.md)

- [使用 R 從模型預測及繪製](tutorials/rtsql-predict-and-plot-from-model.md)

## <a name="step-by-step-tutorials"></a>逐步教學課程

- [如何將機器學習服務和擴充性架構新增至 SQL Server](install/sql-machine-learning-services-windows-install.md)

- [如何從 T-SQL 和預存程序執行 R](tutorials/sqldev-in-database-r-for-sql-developers.md)

- [如何在 Python 中使用內嵌分析](tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="video-introduction"></a>影片介紹

> [!VIDEO https://www.youtube.com/embed/ACejZ9optCQ]

## <a name="reference"></a>參考資料

| 封裝 | 語言 | 描述 |
|:--------|:---------|:------------|
| [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | R | 下列 R 工作的分散式和平行處理：資料轉換、探索、視覺效果、統計和預測性分析。 |
| [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | R | 以 Microsoft AI 演算法為基礎的函式，適用於 R。 |
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | R | 從 OLAP cube.s 匯入資料 |
| [sqlRUtils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | R | 用於封裝 R 和 T-SQL 的協助程式函式。 |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Python | 下列 Python 工作的分散式和平行處理：資料轉換、探索、視覺效果、統計和預測性分析。 |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Python | 以 Microsoft AI 演算法為基礎的函式，適用於 Python。 |
| &nbsp; | &nbsp; | &nbsp; |
