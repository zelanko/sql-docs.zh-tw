---
title: R + T-SQL 教學課程：開發模型
description: 了解如何在 SQL Server 預存程序和 T-SQL 函數中內嵌 R 程式設計語言程式碼。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f0734203a5b5e49ad344b2c0440208c6b652c080
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73725472"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>教學課程：適用於 SQL 開發人員的 R 資料分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這堂專供 SQL 程式設計師參加的教學課程，將說明如何使用 SQL Server 上的 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 資料庫來建置和部署 R 機器學習解決方案，以了解 R 整合。 您將使用 T-SQL、SQL Server Management Studio，以及具有 [機器學習服務]\([機器學習服務](../install/sql-machine-learning-services-windows-install.md)\)和 R 語言支援的資料庫引擎執行個體

本教學課程將為您介紹資料模型化工作流程中所使用的 R 函數。 這些步驟包括資料探索、建置和定型二元分類模型，以及模型部署。 您要建置的模型會根據當天時間、行駛距離及上車地點，預測車程是否會產生小費。 

本教學課程中使用的所有 R 程式碼都會包裝在您透過 Management Studio 建立和執行的預存程序中。

## <a name="background-for-sql-developers"></a>適用於 SQL 開發人員的背景

建置機器學習解決方案的程序很複雜，其中可能牽涉到多項工具，而且需協調數個階段的主題專家：

+ 取得和清除資料
+ 探索資料及建立模型化適用的功能
+ 定型和調整模型
+ 部署到實際執行環境

最好使用專用的 R 開發環境來執行實際程式碼的開發和測試工作。 不過，完整測試指令碼後，您可以在熟悉的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 環境中，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序輕鬆地將它部署至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

這堂涵蓋多個章節的教學課程，主要是介紹將「已完成的 R 程式碼」遷移至 SQL Server 的一般工作流程。 

- [第 1 課：呼叫預存程序中的 R 函數，探索及視覺化資料圖形和分布狀況](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 2 課：在 T-SQL 函數中使用 R 來建立資料特徵](sqldev-create-data-features-using-t-sql.md)
  
- [第 3 課：使用函數和預存程序來定型和儲存 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 4 課：在預存程序中使用 R 模型預測可能的結果](../tutorials/sqldev-operationalize-the-model.md)

將模型儲存至資料庫之後，使用預存程序從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫要預測的模型。

## <a name="prerequisites"></a>Prerequisites

所有工作都可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序來完成。

本教學課程假設您已熟悉基本的資料庫作業，例如建立資料庫和資料表、匯入資料，以及撰寫 SQL 查詢， 但不會假設您已了解 R。因此會提供所有 R 程式碼。 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) 或 [已啟用 R 的 SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 程式庫](../package-management/r-package-information.md)

+ [Permissions](../security/user-permission.md)

+ [紐約市計程車示範資料庫](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用預存程序中的 R 函數探索及視覺化資料](../tutorials/sqldev-explore-and-visualize-the-data.md)
