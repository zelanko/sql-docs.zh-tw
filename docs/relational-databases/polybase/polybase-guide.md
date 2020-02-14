---
title: 什麼是 PolyBase？ | Microsoft Docs
ms.date: 06/10/2019
ms.prod: sql
ms.technology: polybase
ms.topic: overview
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
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions||>=aps-pdw-2016||=azure-sqldw-latest'
ms.openlocfilehash: 7e9e09cece42b84e5fa9691aa0d353d2ed22431b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71710587"
---
# <a name="what-is-polybase"></a>什麼是 PolyBase？

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

<!--SQL Server 2016/2017-->
::: moniker range="= sql-server-2016 || = sql-server-2017 || >= aps-pdw-2016 || = azure-sqldw-latest"

PolyBase 可讓您的 SQL Server 2016 執行個體處理會從 Hadoop 讀取資料的 Transact-SQL 查詢。 相同的查詢也可以存取您 SQL Server 中的關聯式資料表。 PolyBase 也可以讓相同的查詢聯結來自 Hadoop 與 SQL Server 的資料。 在 SQL Server 中，[外部資料表](../../t-sql/statements/create-external-table-transact-sql.md)或[外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md)提供到 Hadoop 的連線。

![PolyBase 邏輯](../../relational-databases/polybase/media/polybase-logical.png "PolyBase 邏輯")

PolyBase 將某些計算推送到 Hadoop 節點以最佳化整體查詢。 不過，PolyBase 外部存取並非僅限於 Hadoop。 也支援其他非結構化資料表，例如分隔文字檔。

> [!TIP]
> SQL Server 2019 引進 PolyBase 的新連接器 (包含 SQL Server、Oracle、Teradata 和 MongoDB)。 如需詳細資訊，請參閱 [SQL Server 2019 的 PolyBase 文件](polybase-guide.md?view=sql-server-ver15)

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

PolyBase 可讓您的 SQL Server 執行個體處理會從外部資料來源讀取資料的 Transact-SQL 查詢。 SQL Server 2016 和更新版本可以存取 Hadoop 和 Azure Blob 儲存體中的外部資料。 從 SQL Server 2019 開始，您現在可以使用 PolyBase 來存取 [SQL Server](polybase-configure-sql-server.md)、[Oracle](polybase-configure-oracle.md)、[Teradata](polybase-configure-teradata.md) 和 [MongoDB](polybase-configure-mongodb.md) 中的外部資料。

存取外部資料的相同查詢也可以將目標設為您 SQL Server 執行個體中的關聯式資料表。 這可讓您結合來自外部來源的資料與資料庫中的高價值關聯式資料。 在 SQL Server 中，[外部資料表](../../t-sql/statements/create-external-table-transact-sql.md)或[外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md)提供到 Hadoop 的連線。

PolyBase 將某些計算推送到 Hadoop 節點以最佳化整體查詢。 不過，PolyBase 外部存取並非僅限於 Hadoop。 也支援其他非結構化資料表，例如分隔文字檔。

::: moniker-end

### <a name="supported-sql-products-and-services"></a>支援的 SQL 產品和服務

PolyBase 為下列 Microsoft SQL 產品提供這些相同的功能：

- SQL Server 2016 和更新版本 (僅限 Windows)
- Analytics Platform System (先前稱為「平行處理資料倉儲」)
- Azure SQL 資料倉儲

### <a name="azure-integration"></a>Azure 整合

有了 PolyBase 在後面的幫助，T-SQL 查詢也可以從 Azure Blob Storage 匯入及匯出資料。 此外，PolyBase 可讓 Azure SQL 資料倉儲從 Azure Data Lake Store 與 Azure Blob 儲存體匯入及匯出資料。

## <a name="why-use-polybase"></a>為何要使用 PolyBase？

過去，很難將您的 SQL Server 資料與外部資料聯結。 您有兩個不好用的選項：

- 傳輸您的一半資料，以便您的所有資料能以一種格式或其他格式表示。
- 同時查詢兩個資料來源，然後撰寫自訂查詢邏輯以在用戶端層級聯結並整合資料。

PolyBase 使用 T-SQL 來聯結資料，讓您不再需要用那種不好用的方式。

為了簡化，PolyBase 不需要在 Hadoop 環境中安裝其他軟體。 您可以使用與用來查詢資料庫資料表相同的 T-SQL 語法來查詢外部資料。 由 PolyBase 所實作的支援動作都同時自動發生。 查詢作者不需要了解 Hadoop。

### <a name="polybase-uses"></a>PolyBase 用途

PolyBase 可在 SQL Server 中啟用下列情節：

- **從 SQL Server 或 PDW 查詢 Hadoop 中所儲存的資料。** 使用者必須將資料儲存於符合成本效益的分散式且可擴充的系統中，例如 Hadoop。 PolyBase 可讓您輕鬆地使用 T-SQL 來查詢資料。

- **查詢 Azure Blob 儲存體中所儲存的資料。** Azure Blob 儲存體是儲存資料以供 Azure 服務使用的便利位置。  PolyBase 可讓您輕鬆地使用 T-SQL 來存取資料。

- **從 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store 匯入資料。** 將 Hadoop 或 Azure Blob 儲存體或 Azure Data Lake Store中的資料匯入至關聯式資料表，以利用 Microsoft SQL 資料行存放區技術和分析功能的速度。 個別 ETL 或匯入工具則不需要。

- **將資料匯出至 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store。** 將資料封存至 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store 以達成符合成本效益的儲存體，並讓它持續上線，方便進行存取。

- **與 BI 工具整合。** 使用 PolyBase 搭配 Microsoft 的商務智慧和分析堆疊，或使用與 SQL Server 相容的任何協力廠商工具。

## <a name="performance"></a>效能

- **將計算推送到 Hadoop。** 查詢最佳化工具會做出成本型決策，以將計算推送到 Hadoop，而這麼做可以改善查詢效能。  它使用外部資料表上的統計資料來做出成本型決策。 推送計算會建立 MapReduce 工作，並利用 Hadoop 的分散式運算資源。

- **調整計算資源。** 若要改善查詢效能，您可以使用 SQL Server [PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)。 這可啟用 SQL Server 執行個體與 Hadoop 節點之間的平行資料傳輸，而且會加入在外部資料上運作的計算資源。

<!--SQL Server 2016/2017-->
::: moniker range="=sql-server-2016||=sql-server-2017"

## <a name="next-steps"></a>後續步驟

使用 PolyBase 之前，您必須[安裝 PolyBase 功能](polybase-installation.md)。 然後請參閱下列設定指南 (視您的資料來源) 而定：

- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob 儲存體](polybase-configure-azure-blob-storage.md)

::: moniker-end
<!--SQL Server 2019-->
::: moniker range=">= sql-server-linux-ver15||>= sql-server-ver15||=sqlallproducts-allversions"

## <a name="next-steps"></a>後續步驟

使用 PolyBase 之前，您必須[安裝 PolyBase 功能](polybase-installation.md)。 然後請參閱下列設定指南 (視您的資料來源) 而定：
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob 儲存體](polybase-configure-azure-blob-storage.md)
- [SQL Server](polybase-configure-sql-server.md)
- [Oracle](polybase-configure-oracle.md)
- [Teradata](polybase-configure-teradata.md)
- [MongoDB](polybase-configure-mongodb.md)
- [ODBC 泛型型別](polybase-configure-odbc-generic.md)

::: moniker-end
