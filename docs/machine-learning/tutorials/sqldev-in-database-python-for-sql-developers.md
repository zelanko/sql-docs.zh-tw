---
title: Python + T-SQL：開發模型
description: 了解如何在 SQL Server 預存程序和 T-SQL 函數中內嵌 Python 程式碼。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d5cdec0ad291fecf0606650d116f0c7979831c19
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785635"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>教學課程：適用於 SQL 開發人員的 Python 資料分析
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

這堂專供 SQL 程式設計師參加的教學課程，將說明使用 SQL Server 上的 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 資料庫來建置和部署 Python 機器學習解決方案，以了解 Python 整合。 您將使用 T-SQL、SQL Server Management Studio，以及具有[機器學習服務](../install/sql-machine-learning-services-windows-install.md)和 Python 語言支援的資料庫引擎執行個體。

本教學課程將為您介紹資料模型化工作流程中所使用的 Python 函數。 這些步驟包括資料探索、建置和定型二元分類模型，以及模型部署。 您將使用紐約市計程車委員會 (New York City Taxi and Limosine Commission) 提供的範例資料，而您要建置的模型會根據當天時間、行駛距離及上車地點，預測車程是否會產生小費。 

本教學課程中使用的所有 Python 程式碼都會包裝在您透過 Management Studio 建立和執行的預存程序中。

> [!NOTE]
> 這個教學課程適用於 R 和 Python。 如需 R 版本，請參閱[適用於 R 開發人員的資料庫內分析](sqldev-in-database-r-for-sql-developers.md)。

## <a name="overview"></a>概觀

建置機器學習解決方案的程序很複雜，其中可能牽涉到多項工具，而且需協調數個階段的主題專家：

+ 取得和清除資料
+ 探索資料及建立模型化適用的功能
+ 定型和調整模型
+ 部署到實際執行環境

最好使用專用的開發環境來執行實際程式碼的開發和測試工作。 不過，完整測試指令碼後，您可以在熟悉的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 環境中，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序輕鬆地將它部署至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 將外部程式碼包裝在預存程序裡，是運用 SQL Server 中程式碼的主要機制。

無論您是剛接觸 Python 的 SQL 程式設計師，或是剛接觸 SQL 的 Python 開發人員，這堂涵蓋多個章節的教學課程都會介紹如何使用 Python 和 SQL Server 執行資料庫內分析的一般工作流程。 

+ [第 1 課：使用 Python 探索及視覺化資料](sqldev-py3-explore-and-visualize-the-data.md)

+ [第 2 課：使用自訂 SQL 函數，建立資料特徵](sqldev-py4-create-data-features-using-t-sql.md)

+ [第 3 課：使用 T-SQL 定型及儲存 Python 模型](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [第 4 課：在預存程序中使用 Python 模型預測可能的結果](sqldev-py6-operationalize-the-model.md)

將模型儲存至資料庫之後，您可以使用預存程序從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫要預測的模型。

## <a name="prerequisites"></a>Prerequisites

+ [使用 Python 的 SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [權限](../security/user-permission.md)

+ [紐約市計程車示範資料庫](demo-data-nyctaxi-in-sql.md)

所有工作都可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序來完成。

本教學課程假設您已熟悉基本的資料庫作業，例如建立資料庫和資料表、匯入資料，以及撰寫 SQL 查詢， 但不會假設您已了解 Python。 因此會提供所有 Python 程式碼。 

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 Python 探索及視覺化資料](sqldev-py3-explore-and-visualize-the-data.md)
