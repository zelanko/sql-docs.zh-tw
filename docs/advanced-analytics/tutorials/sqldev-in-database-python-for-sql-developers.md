---
title: 適用於 SQL 開發人員-SQL Server 機器學習服務的資料庫內 Python 分析的教學課程
description: 了解如何在 SQL Server 預存程序和 T-SQL 函式中內嵌 Python 程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e036aa2a4c104eaf92e3e9aaf4513f2542bf23b4
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511685"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>教學課程：適用於 SQL 開發人員的 Python 資料分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本教學課程中的 SQL 程式設計人員，透過建置和部署以 Python 為基礎的機器學習解決方案使用了解 Python 整合[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)上 SQL Server 資料庫。 您將使用 T-SQL、 SQL Server Management Studio，並使用 database engine 執行個體[Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md)和 Python 語言支援。

本教學課程會向您介紹的資料模型化工作流程中使用的 Python 函式。 步驟包括資料瀏覽、 建置及定型二元分類模型和部署模型。 您會使用從 New York City 計程車和 Limosine 佣金，範例資料，您將建置的模型會預測一趟車程是否可能會造成提示，根據的時間、 歷經一段，距離和上車位置中。 

在本教學課程中使用的 Python 程式碼的所有包裝在您建立和在 Management Studio 中執行的預存程序。

> [!NOTE]
> 本教學課程適用於 R 和 Python。 R 版本，請參閱[資料庫內分析適用於 R 開發人員](sqldev-in-database-r-for-sql-developers.md)。

## <a name="overview"></a>總覽

建置機器學習服務解決方案的程序很複雜，可包含多個工具和專家協調跨數個階段：

+ 取得和清除資料
+ 瀏覽資料及建置適用於模型化功能
+ 定型和微調模型
+ 部署至生產環境

實際的程式碼的開發和測試是最適合執行使用專用的開發環境。 不過，指令碼經過完整測試之後，您可以輕鬆部署到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序在熟悉的環境中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 外部程式碼包裝在預存程序是運用 SQL Server 中的程式碼的主要機制。

不論您是剛接觸 Python 或 Python 開發人員熟悉 SQL 的 SQL 程式設計人員，此多部分的教學課程會介紹進行 Python 和 SQL Server 資料庫內分析的一般工作流程。 

+ [第 1 課：瀏覽及視覺化資料使用 Python](sqldev-py3-explore-and-visualize-the-data.md)

+ [第 2 課：使用自訂 SQL 函式建立資料特徵](sqldev-py4-create-data-features-using-t-sql.md)

+ [第 3 課：訓練及儲存使用 T-SQL Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [第 4 課：預測潛在的預存程序中使用 Python 模型的結果](sqldev-py6-operationalize-the-model.md)

模型儲存到資料庫之後，您可以呼叫模型的預測[!INCLUDE[tsql](../../includes/tsql-md.md)]使用預存程序。

## <a name="prerequisites"></a>先決條件

+ [SQL Server 2017 Machine Learning 服務與 Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Permissions](../security/user-permission.md)

+ [NYC 計程車示範資料庫](demo-data-nyctaxi-in-sql.md)

所有的工作可使用[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

本教學課程假設您熟悉基本資料庫作業，例如建立資料庫和資料表、 匯入資料，以及撰寫 SQL 查詢。 它不會假設您知道 Python。 此情況下，會提供所有的 Python 程式碼。 

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [瀏覽及視覺化資料使用 Python](sqldev-py3-explore-and-visualize-the-data.md)
