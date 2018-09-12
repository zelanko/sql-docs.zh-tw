---
title: PolyBase 指南 | Microsoft Docs
ms.date: 05/31/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: quickstart
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- Hadoop import
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c31f9538f3429ff4ae1182ee0cd974996cc705a6
ms.sourcegitcommit: 82bb56269faf3fb5dd1420418e32a0a6476780cc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2018
ms.locfileid: "43694721"
---
# <a name="polybase-guide"></a>PolyBase 指南

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

PolyBase 可讓您的 SQL Server 2016 執行個體處理會從 Hadoop 讀取資料的 Transact-SQL 查詢。 相同的查詢也可以存取您 SQL Server 中的關聯式資料表。 PolyBase 也可以讓相同的查詢聯結來自 Hadoop 與 SQL Server 的資料。 在 SQL Server 中，[外部資料表](../../t-sql/statements/create-external-table-transact-sql.md)或[外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md)提供到 Hadoop 的連線。

PolyBase 為下列 Microsoft SQL 產品提供這些相同的功能：

- SQL Server 2016 與更新版本
- Analytics Platform System (先前稱為「平行處理資料倉儲」)
- Azure SQL 資料倉儲

PolyBase 將某些計算推送到 Hadoop 節點以最佳化整體查詢。 不過，PolyBase 外部存取並非僅限於 Hadoop。 也支援其他非結構化資料表，例如分隔文字檔。

#### <a name="data-import-and-export"></a>資料匯入及匯出

有了 PolyBase 在後面的幫助，T-SQL 查詢也可以從 Azure Blob Storage 匯入及匯出資料。 此外，PolyBase 可讓 Azure SQL 資料倉儲從 Azure Data Lake Store 與 Azure Blob 儲存體匯入及匯出資料。

若要使用 PolyBase，請參閱 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)。
  
![PolyBase 邏輯](../../relational-databases/polybase/media/polybase-logical.png "PolyBase 邏輯")

## <a name="why-use-polybase"></a>為何要使用 PolyBase？

過去，很難將您的 SQL Server 資料與外部資料聯結。 您有兩個不好用的選項：

- 傳輸您的一半資料，以便您的所有資料能以一種格式或其他格式表示。
- 同時查詢兩個資料來源，然後撰寫自訂查詢邏輯以在用戶端層級聯結並整合資料。

PolyBase 使用 T-SQL 來聯結資料，讓您不再需要用那種不好用的方式

為了簡化，PolyBase 不需要在 Hadoop 環境中安裝其他軟體。 您可以使用與用來查詢資料庫資料表相同的 T-SQL 語法來查詢外部資料。 由 PolyBase 所實作的支援動作都同時自動發生。 查詢作者不需要了解 Hadoop。

PolyBase 可以：

- **從 SQL Server 或 PDW 查詢 Hadoop 中所儲存的資料。** 使用者必須將資料儲存於符合成本效益的分散式且可擴充的系統中，例如 Hadoop。 PolyBase 可讓您輕鬆地使用 T-SQL 來查詢資料。

- **查詢 Azure Blob 儲存體中所儲存的資料。** Azure Blob 儲存體是儲存資料以供 Azure 服務使用的便利位置。  PolyBase 可讓您輕鬆地使用 T-SQL 來存取資料。

- **從 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store 匯入資料。** 將 Hadoop 或 Azure Blob 儲存體或 Azure Data Lake Store中的資料匯入至關聯式資料表，以利用 Microsoft SQL 資料行存放區技術和分析功能的速度。 個別 ETL 或匯入工具則不需要。

- **將資料匯出至 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store。** 將資料封存至 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store 以達成符合成本效益的儲存體，並讓它持續上線，方便進行存取。

- **與 BI 工具整合。** 使用 PolyBase 搭配 Microsoft 的商務智慧和分析堆疊，或使用與 SQL Server 相容的任何協力廠商工具。

## <a name="performance"></a>效能

- **將計算推送到 Hadoop。** 查詢最佳化工具會做出成本型決策，以將計算推送到 Hadoop，而這麼做可以改善查詢效能。  它使用外部資料表上的統計資料來做出成本型決策。 推送計算會建立 MapReduce 工作，並利用 Hadoop 的分散式運算資源。

- **調整計算資源。** 若要改善查詢效能，您可以使用 SQL Server [PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)。 這可啟用 SQL Server 執行個體與 Hadoop 節點之間的平行資料傳輸，而且會加入在外部資料上運作的計算資源。

## <a name="polybase-guide-topics"></a>PolyBase 指南主題

本指南包含可協助您有效率且有效地使用 PolyBase 的主題。

|||
|-|-|
|**主題**|**描述**|
|[開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)|安裝和設定 PolyBase 的基本步驟。 這會顯示如何建立指向 Hadoop 或 Azure Blob 儲存體中資料的外部物件，並提供查詢範例。|
|[PolyBase 建立版本的功能摘要](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|描述 SQL Server、SQL Database 和 SQL Data Warehouse 支援的 PolyBase 功能。|
|[PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)|使用 SQL Server 向外延展群組，以向外延展 SQL Server 與 Hadoop 之間的平行處理原則。|
|[安裝 PolyBase](../../relational-databases/polybase/polybase-installation.md)|使用安裝精靈或命令列工具安裝 PolyBase 的參考和步驟。|
|[PolyBase 設定](../../relational-databases/polybase/polybase-configuration.md)|設定 PolyBase 的 SQL Server 設定。  例如，設定計算下推和 Kerberos 安全性。|
|[PolyBase T-SQL 物件](../../relational-databases/polybase/polybase-t-sql-objects.md)|建立 PolyBase 用來定義和存取外部資料的 T-SQL 物件。|
|[PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)|使用 T-SQL 陳述式查詢、匯入或匯出外部資料。|
|[PolyBase, 疑難排解](../../relational-databases/polybase/polybase-troubleshooting.md)|管理 PolyBase 查詢的技術。 使用動態管理檢視 (DMV) 來監視 PolyBase 查詢，並了解如何讀取 PolyBase 查詢計劃來找出效能瓶頸。|
| &nbsp; | &nbsp; |
  
