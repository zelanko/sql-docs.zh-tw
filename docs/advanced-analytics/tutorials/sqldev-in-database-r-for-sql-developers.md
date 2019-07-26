---
title: 使用 R 進行資料庫內分析的教學課程
description: 瞭解如何在 SQL Server 預存程式和 T-sql 函數中內嵌 R 程式設計語言程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1257cc3f3d0b3ed07bc879f5bc3337d62bc1b3a0
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470577"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>教學課程：適用于 SQL 開發人員的 R 資料分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在適用于 SQL 程式設計人員的本教學課程中, 您可以使用 SQL Server 上的[NYCTaxi_sample](demo-data-nyctaxi-in-sql.md)資料庫來建立和部署 r 型機器學習服務解決方案, 以瞭解 r 整合。 您將使用 T-sql、SQL Server Management Studio 和資料庫引擎實例搭配 [Machine Learning Services] ([Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)和 R 語言支援

本教學課程將為您介紹資料模型化工作流程中使用的 R 函數。 步驟包括資料探索、建立和定型二元分類模型, 以及模型部署。 您將建立的模型會預測旅程是否可能會根據當天時間、旅遊距離和挑選位置來產生提示。 

本教學課程中使用的所有 R 程式碼都會包裝在您建立並在 Management Studio 中執行的預存程式中。

## <a name="background-for-sql-developers"></a>SQL 開發人員的背景

建立機器學習解決方案的程式是一種複雜的程式, 其中可能牽涉到多項工具, 並協調主題專家跨越數個階段:

+ 取得和清除資料
+ 探索資料和建立適用于模型化的功能
+ 定型和調整模型
+ 部署至生產環境

實際程式碼的開發和測試, 最好是使用專用的 R 開發環境來執行。 不過, 在腳本經過完整測試之後, 您就可以輕鬆地將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]它[!INCLUDE[tsql](../../includes/tsql-md.md)]部署到熟悉的環境[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中使用預存程式。

本多部分教學課程的目的是將「已完成 R 程式碼」遷移至 SQL Server 的一般工作流程簡介。 

- [第 1 課：藉由呼叫預存程式中的 R 函式, 探索及視覺化資料圖形和散發](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 2 課：在 T-sql 函數中使用 R 建立資料特徵](sqldev-create-data-features-using-t-sql.md)
  
- [第 3 課：使用函數和預存程式來定型和儲存 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 4 課：在預存程式中使用 R 模型來預測潛在結果](../tutorials/sqldev-operationalize-the-model.md)

將模型儲存至資料庫之後, 使用預存程式從[!INCLUDE[tsql](../../includes/tsql-md.md)]呼叫模型以取得預測。

## <a name="prerequisites"></a>必要條件

所有工作都可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]預存程式來完成。

本教學課程假設您已熟悉基本資料庫作業, 例如建立資料庫和資料表、匯入資料, 以及撰寫 SQL 查詢。 它不會假設您知道 R。因此, 會提供所有 R 程式碼。 

+ 已啟用 R 的[SQL Server 2016 R services](../install/sql-r-services-windows-install.md#verify-installation)或[SQL Server 2017 Machine Learning 服務](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 程式庫](../package-management/installed-package-information.md)

+ [Permissions](../security/user-permission.md)

+ [NYC 計程車示範資料庫](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用預存程式中的 R 函數探索資料並加以視覺化](../tutorials/sqldev-explore-and-visualize-the-data.md)
