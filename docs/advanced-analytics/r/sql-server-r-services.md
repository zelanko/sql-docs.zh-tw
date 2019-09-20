---
title: 什麼是 SQL Server 2016 R 服務？
titleSuffix: ''
description: R Services 是 SQL Server 2016 中的一項功能，可讓您以關聯式資料執行 R 腳本。 您可以使用開放原始碼套件和架構，以及適用于預測性分析和機器學習的 Microsoft R 套件。 指令碼會在資料庫中執行，不需在 SQL Server 外部或透過網路來移動資料。 本文說明 SQL Server R Services 的基本概念。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/12/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 99aba9748e7ee6d53aabb18919324243740d996a
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149927"
---
# <a name="what-is-sql-server-2016-r-services"></a>什麼是 SQL Server 2016 R 服務？
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R Services 是 SQL Server 2016 中的一項功能，可讓您以關聯式資料執行 R 腳本。 您可以使用開放原始碼套件和架構，以及適用于預測性分析和機器學習的[Microsoft R 套件](#packages)。 指令碼會在資料庫中執行，不需在 SQL Server 外部或透過網路來移動資料。 本文說明 SQL Server R Services 的基本概念。

> [!Note]
> R 服務已在 SQL Server 2017 和更新版本中重新命名為[Machine Learning 服務](../what-is-sql-server-machine-learning.md)，並同時支援 Python 和 R。

## <a name="what-is-r-services"></a>什麼是 R 服務？

SQL Server R Services 可讓您執行資料庫內的 R 腳本。 您可以使用它來準備和清除資料、進行功能工程設計，以及在資料庫中定型、評估和部署機器學習模型。 此功能會在資料所在的位置執行您的腳本，並消除透過網路傳送資料到另一部伺服器的情況。

R 的基底散發套件包含在 R Services 中。 除了 Microsoft 封裝[RevoScaleR](../r/ref-r-revoscaler.md)、 [MicrosoftML](../r/ref-r-microsoftml.md)、[olapR] 之外，您還可以使用開放原始碼套件和架構。/r/ref-r-olapr.md），以及適用于 R 的[sqlrutils](../r/ref-r-sqlrutils.md) 。

R Services 會使用擴充性架構，在 SQL Server 中執行 R 腳本。 深入瞭解其運作方式：

+ [擴充性架構](../concepts/extensibility-framework.md)
+ [R 擴充功能](../concepts/extension-r.md)

## <a name="what-can-i-do-with-r-services"></a>我可以使用 R Services 做什麼？

您可以使用 R Services，在 SQL Server 內建立和定型機器學習和深度學習模型。 您也可以將現有的模型部署至 R 服務，並使用關聯式資料進行預測。

您可以使用 SQL Server R Services 的預測類型範例包括：

|||
|-|-|
|分類/分類|自動將客戶意見分割成正面和負面的類別|
|回歸/預測連續值|根據大小和位置來預測房屋價格|
|異常偵測|偵測詐騙銀行交易 |
|建議|根據先前的購買專案, 建議線上購物者可能想要購買的產品|

### <a name="how-to-execute-r-scripts"></a>如何執行 R 腳本

有兩種方式可以在 R Services 中執行 R 腳本：

+ 最常見的方式是使用 T-sql 預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 您也可以使用慣用的 R 用戶端，並撰寫將執行（稱為*遠端計算內容*）推送至遠端 SQL Server 的腳本。 如需詳細資訊，請參閱如何[設定資料科學用戶端開發](../r/set-up-a-data-science-client.md)。

<a name="packages"></a>

## <a name="r-packages"></a>R 套件

除了 Microsoft 的企業套件以外，您還可以使用開放原始碼套件和架構。 最常見的開放原始碼 R 套件會預先安裝在 R Services 中。 Microsoft 的下列 R 套件也包含在內：

| 套件 | 描述 |
|-|-|
| [RevoScaleR](../r/ref-r-revoscaler.md) | 可調整 R 的主要套件。資料轉換和操作、統計摘要、視覺效果，以及許多形式的模型化。 此外，此套件中的函式會自動將工作負載分散到可用的核心，以進行平行處理。 |
| [MicrosoftML （R）](../r/ref-r-microsoftml.md) | 新增機器學習演算法，以建立文字分析、影像分析和情感分析的自訂模型。 |
| [olapR](../r/ref-r-olapr.md) | 用於對 SQL Server Analysis Services OLAP Cube 進行 MDX 查詢的 R 函數。 |
| [sqlrutils](../r/ref-r-sqlrutils.md) | 在 T-sql 預存程式中使用 R 腳本的機制、向資料庫註冊該預存程式，以及從[R 開發環境](../r/set-up-a-data-science-client.md)執行預存程式。 |
| [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open （MRO）是由 Microsoft 加強的 R 散發。 這是適用于統計分析和資料科學的完整開放原始碼平臺。 它是以與 R 相容的 100% 為基礎，並包含改善效能和重現性的其他功能。 |

## <a name="how-do-i-get-started-with-rservices"></a>如何? 開始使用 RServices？

1. [安裝 SQL Server 2016 R 服務](../install/sql-r-services-windows-install.md)

1. 設定您的開發工具。 您可以使用：

    + [Azure Data Studio](../../azure-data-studio/what-is.md)或[SQL Server Management Studio （SSMS）](../../ssms/sql-server-management-studio-ssms.md)來使用 t-sql 和預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)來執行 R 腳本。
    + R 在您自己的開發膝上型電腦或工作站上執行腳本。 您可以使用[RevoScaleR](../r/ref-r-revoscaler.md)將資料提取到本機，或從遠端將執行推送至 SQL Server。 如需詳細資訊，請參閱如何[設定資料科學用戶端開發](../r/set-up-a-data-science-client.md)。

1. 撰寫您的第一個 R 腳本

    + 快速入門：[在 SQL Server 中建立和執行簡單的 R 腳本](../tutorials/quickstart-r-create-script.md)
    + 快速入門：[在 R 中建立和定型預測模型](../tutorials/quickstart-r-train-score-model.md)
    + 教學課程：[在 t-sql 中使用 R](../tutorials/sqldev-in-database-r-for-sql-developers.md)：探索資料、執行特徵工程設計、定型和部署模型，以及進行預測（五個部分的系列）
    + 教學課程：[在 r 工具中使用 r Services](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)：流覽資料、建立圖形和繪圖、執行特徵工程設計、定型和部署模型，以及進行預測（六個部分的系列）

## <a name="next-steps"></a>後續步驟

+ [安裝 SQL Server 2016 R 服務](../install/sql-r-services-windows-install.md)
+ [設定適用于 R 開發的資料科學用戶端](../r/set-up-a-data-science-client.md)