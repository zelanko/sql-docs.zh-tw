---
title: 適用于 SQL 開發人員的資料庫內 Python 分析教學課程
description: 瞭解如何在 SQL Server 預存程式和 T-sql 函數中內嵌 Python 程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6147c4670dace104c2c33c19e1fd29cbf2d4f2ee
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468857"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>教學課程：適用于 SQL 開發人員的 Python 資料分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在適用于 SQL 程式設計人員的本教學課程中, 瞭解如何使用 SQL Server 上的[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)資料庫來建立及部署以 python 為基礎的機器學習服務解決方案, 以瞭解 python 整合。 您將使用 T-sql、SQL Server Management Studio, 以及具有[Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)和 Python 語言支援的資料庫引擎實例。

本教學課程將為您介紹資料模型化工作流程中使用的 Python 函式。 步驟包括資料探索、建立和定型二元分類模型, 以及模型部署。 您將使用來自紐約計程車和 Limosine 委員會的範例資料, 而您將建立的模型會預測旅程是否可能會根據當天時間、距離行駛和挑選位置來產生秘訣。 

本教學課程中使用的所有 Python 程式碼都會包裝在您建立並在 Management Studio 中執行的預存程式中。

> [!NOTE]
> 本教學課程適用于 R 和 Python。 如需 R 版本, 請參閱[適用于 r 開發人員的資料庫內分析](sqldev-in-database-r-for-sql-developers.md)。

## <a name="overview"></a>總覽

建立機器學習解決方案的程式是一種複雜的程式, 其中可能牽涉到多項工具, 並協調主題專家跨越數個階段:

+ 取得和清除資料
+ 探索資料和建立適用于模型化的功能
+ 定型和調整模型
+ 部署至生產環境

實際程式碼的開發和測試, 最好是使用專用的開發環境來執行。 不過, 在腳本經過完整測試之後, 您就可以輕鬆地將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]它[!INCLUDE[tsql](../../includes/tsql-md.md)]部署到熟悉的環境[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中使用預存程式。 將外部程式碼包裝在預存程式中, 是在 SQL Server 中運用程式碼的主要機制。

無論您是 Python 的 SQL 程式設計人員新手, 或 SQL 的 Python developer 新手, 這個多部分的教學課程都會介紹使用 Python 和 SQL Server 進行資料庫內分析的一般工作流程。 

+ [第 1 課：使用 Python 探索資料並加以視覺化](sqldev-py3-explore-and-visualize-the-data.md)

+ [第 2 課：使用自訂 SQL 函數建立資料特徵](sqldev-py4-create-data-features-using-t-sql.md)

+ [第 3 課：使用 T-sql 定型及儲存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [第 4 課：在預存程式中使用 Python 模型來預測潛在結果](sqldev-py6-operationalize-the-model.md)

將模型儲存至資料庫之後, 您可以使用預存程式, 從[!INCLUDE[tsql](../../includes/tsql-md.md)]呼叫模型以取得預測。

## <a name="prerequisites"></a>先決條件

+ [使用 Python SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [Permissions](../security/user-permission.md)

+ [NYC 計程車示範資料庫](demo-data-nyctaxi-in-sql.md)

所有工作都可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]預存程式來完成。

本教學課程假設您已熟悉基本資料庫作業, 例如建立資料庫和資料表、匯入資料, 以及撰寫 SQL 查詢。 它不會假設您知道 Python。 因此, 會提供所有 Python 程式碼。 

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 Python 探索資料並加以視覺化](sqldev-py3-explore-and-visualize-the-data.md)
