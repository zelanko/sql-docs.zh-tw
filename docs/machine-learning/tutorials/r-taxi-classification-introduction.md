---
title: R 教學課程：使用二元分類預測紐約市計程車車資
titleSuffix: SQL machine learning
description: 在這五部分的教學課程系列中，您將了解如何使用 SQL 機器學習將 R 程式碼內嵌在 SQL Server 預存程序和 T-SQL 函式中，以使用二元分類來預測紐約市計程車車資。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: db8a0c073821df46e6d9d5bda43e74aae19a2501
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2020
ms.locfileid: "94585028"
---
# <a name="r-tutorial-predict-nyc-taxi-fares-with-binary-classification"></a>R 教學課程：使用二元分類預測紐約市計程車車資
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
在 SQL 程式設計人員的這個五部分教學課程系列中，您將了解 [SQL Server 機器學習服務](../sql-server-machine-learning-services.md)中或[巨量資料叢集](../../big-data-cluster/machine-learning-services.md)上的 R 整合。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
在 SQL 程式設計人員的這個五部分教學課程系列中，您將了解 [SQL Server 機器學習服務](../sql-server-machine-learning-services.md)中的 R 整合。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
在 SQL 程式設計人員的這個五部分教學課程系列中，您將了解 [SQL Server 2016 R Services](../sql-server-machine-learning-services.md) 中的 R 整合。
::: moniker-end

::: moniker range=">=azuresqldb-mi-current||=sqlallproducts-allversions"
在 SQL 程式設計人員的這個五部分教學課程系列中，您將了解 [Azure SQL 受控執行個體中機器學習服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)中的 R 整合。
::: moniker-end

您將使用 SQL Server 上的範例資料庫，建置和部署以 R 為基礎的機器學習解決方案。 您將使用 T-SQL、Azure Data Studio 或 SQL Server Management Studio，以及具有 SQL 機器學習和 R 語言支援的資料庫引擎執行個體

本教學課程系列將為您介紹資料模型化工作流程中所使用的 R 函式。 其中包括資料探索、建置和定型二元分類模型，以及模型部署。 您將使用紐約市計程車和禮車委員會的範例資料。 您將建置的模型會根據當天時間、行駛距離及上車地點，預測車程是否會產生小費。

在此系列課程的第一部分中，您將安裝必要條件和還原範例資料庫。 在第二部分和第三部分中，您將開發一些 R 指令碼來準備您的資料，並將機器學習模型定型。 接著，在第四和第五部分中，您將使用 T-SQL 預存程序執行資料庫中的這些 R 指令碼。

在本文中，您將：

> [!div class="checklist"]
> + 安裝先決條件
> + 還原範例資料庫

在[第二部分](r-taxi-classification-explore-data.md)中，您將探索範例資料並產生繪圖。

在[第三部分](r-taxi-classification-create-features.md)中，您將了解如何使用 Transact-SQL 函式，從未經處理的資料建立特徵。 接著您將從預存程序呼叫該函數，以建立包含特徵值的資料表。

在[第四部分](r-taxi-classification-train-model.md)中，您將載入模組，並呼叫所需的函式，以使用 SQL Server 預存程序來建立和定型模型。

在[第五部分](r-taxi-classification-deploy-model.md)中，您將了解如何運作您在第四部分中定型並儲存的模型。

> [!NOTE]
> 這個教學課程適用於 R 和 Python。 針對 Python 版本，請參閱 [Python 教學課程：使用二元分類預測紐約市計程車車資](r-taxi-classification-introduction.md)。

## <a name="prerequisites"></a>必要條件

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
+ 安裝 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation)
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ 安裝[啟用 R 的 SQL Server 機器學習服務](../install/sql-machine-learning-services-windows-install.md#verify-installation)
::: moniker-end

+ 安裝 [R 程式庫](../package-management/r-package-information.md)

+ [授與執行 Python 指令碼的權限](../security/user-permission.md)

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ 從 SQL Server 2019 開始，隔離機制會要求您授與繪圖檔案儲存所在目錄的適當權限。 如需有關如何設定這些權限的詳細資訊，請參閱 [Windows 上 SQL Server 2019 中的檔案權限區段：機器學習服務的隔離變更](../install/sql-server-machine-learning-services-2019.md#file-permissions)
::: moniker-end

+ 還原[紐約市計程車示範資料庫](demo-data-nyctaxi-in-sql.md)

所有工作都可以使用 Azure Data Studio 獲 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序來完成。

本教學課程假設您已熟悉基本的資料庫作業，例如建立資料庫和資料表、匯入資料，以及撰寫 SQL 查詢， 但不會假設您已了解 R。因此會提供所有 R 程式碼。

## <a name="background-for-sql-developers"></a>適用於 SQL 開發人員的背景

建置機器學習解決方案的程序很複雜，其中可能牽涉到多項工具，而且需協調數個階段的主題專家：

+ 取得和清除資料
+ 探索資料及建立模型化適用的功能
+ 定型和調整模型
+ 部署到實際執行環境

最好使用專用的 R 開發環境來執行實際程式碼的開發和測試工作。 不過，完整測試指令碼後，您可以在熟悉的 Azure Data Studio 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 環境中，使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序輕鬆將其部署至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 將外部程式碼包裝在預存程序裡，是運用 SQL Server 中程式碼的主要機制。

將模型儲存至資料庫之後，您可以使用預存程序從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫要預測的模型。

無論您是剛接觸 R 的 SQL 程式設計人員，還是剛接觸 SQL 的 R 開發人員新手，這五個部分的教學課程系列介紹的一般工作流程，都可引導您了解如何使用 R 和 SQL Server 執行資料庫內分析。

## <a name="next-steps"></a>後續步驟

在本文章中，您將：

> [!div class="checklist"]
> + 已安裝必要條件
> + 已還原範例資料庫

> [!div class="nextstepaction"]
> [R 教學課程：探索及視覺化資料](r-taxi-classification-explore-data.md)