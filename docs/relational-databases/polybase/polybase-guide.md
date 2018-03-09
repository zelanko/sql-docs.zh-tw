---
title: "PolyBase 指南 | Microsoft Docs"
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: get-started-article
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- "Hadoop import ×"
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 13f4dc7e877341917ebf4f41694cb886c81c53f2
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="polybase-guide"></a>PolyBase 指南
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
PolyBase 是一種技術，可透過 t-sql 語言存取資料庫外部的資料。  在 SQL Server 2016 中，它可讓您對 Hadoop 中的外部資料執行查詢，或從 Azure Blob 儲存體匯入/匯出資料。 查詢已最佳化，可將計算推送到 Hadoop。 在 Azure SQL 資料倉儲中，您可以從 Azure Blob 儲存體和 Azure Data Lake Store 中匯入/匯出資料。
  
  
 若要使用 PolyBase，請參閱 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 ![PolyBase 邏輯](../../relational-databases/polybase/media/polybase-logical.png "PolyBase 邏輯")  
  
## <a name="why-use-polybase"></a>為何要使用 PolyBase？  
若要做出不錯的決策，您要將關聯式資料和其他非結構化資料分析為資料表 (尤其是 Hadoop)。 除非您有方法可在不同類型的資料存放區之間傳送資料，否則這不容易達成。 PolyBase 透過對 SQL Server 外部資料進行操作來縮短這個差距。  
  
為了簡化，PolyBase 不需要在 Hadoop 環境中安裝其他軟體。 查詢外部資料與查詢資料庫資料表所使用的語法相同。 這都會以透明方式進行。 PolyBase 會處理幕後的所有詳細資料，而且使用者不需具備 Hadoop 的知識就能查詢外部資料表。 
  
 PolyBase 可以：  
  
-   **從 SQL Server 或 PDW 查詢 Hadoop 中所儲存的資料。** 使用者必須將資料儲存於符合成本效益的分散式且可擴充的系統中，例如 Hadoop。 PolyBase 可讓您輕鬆地使用 T-SQL 來查詢資料。  
  
-   **查詢 Azure Blob 儲存體中所儲存的資料。** Azure Blob 儲存體是儲存資料以供 Azure 服務使用的便利位置。  PolyBase 可讓您輕鬆地使用 T-SQL 來存取資料。  
  
-   **將資料從 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store 匯入** 將資料從 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store 匯入至關聯式資料表，以利用 Microsoft SQL 資料行存放區技術和分析功能的速度。 個別 ETL 或匯入工具則不需要。  

-   **將資料匯出至 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store。** 將資料封存至 Hadoop、Azure Blob 儲存體或 Azure Data Lake Store 以達成符合成本效益的儲存體，並讓它持續上線，方便進行存取。  
  
-   **與 BI 工具整合。** 使用 PolyBase 搭配 Microsoft 的商務智慧和分析堆疊，或使用與 SQL Server 相容的任何協力廠商工具。  
  
## <a name="performance"></a>[效能]  
  
-   **將計算推送到 Hadoop。**查詢最佳化工具會做出成本型決策，以將計算推送到 Hadoop，而這麼做可以改善查詢效能。  它使用外部資料表上的統計資料來做出成本型決策。 推送計算會建立 MapReduce 工作，並利用 Hadoop 的分散式運算資源。  
  
-   **調整計算資源。** 若要改善查詢效能，您可以使用 SQL Server [PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)。 這可啟用 SQL Server 執行個體與 Hadoop 節點之間的平行資料傳輸，而且會加入在外部資料上運作的計算資源。  
  
## <a name="polybase-guide-topics"></a>PolyBase 指南主題  
 本指南包含可協助您有效率且有效地使用 PolyBase 的主題。  
  
|||  
|-|-|  
|**主題**|**說明**|  
|[開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)|安裝和設定 PolyBase 的基本步驟。 這會顯示如何建立指向 Hadoop 或 Azure Blob 儲存體中資料的外部物件，並提供查詢範例。|  
|[PolyBase 建立版本的功能摘要](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|描述 SQL Server、SQL Database 和 SQL Data Warehouse 支援的 PolyBase 功能。|  
|[PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)|使用 SQL Server 向外延展群組，以向外延展 SQL Server 與 Hadoop 之間的平行處理原則。|  
|[安裝 PolyBase](../../relational-databases/polybase/polybase-installation.md)|使用安裝精靈或命令列工具安裝 PolyBase 的參考和步驟。|  
|[PolyBase 設定](../../relational-databases/polybase/polybase-configuration.md)|設定 PolyBase 的 SQL Server 設定。  例如，設定計算下推和 Kerberos 安全性。|  
|[PolyBase T-SQL 物件](../../relational-databases/polybase/polybase-t-sql-objects.md)|建立 PolyBase 用來定義和存取外部資料的 T-SQL 物件。|  
|[PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)|使用 T-SQL 陳述式查詢、匯入或匯出外部資料。|  
|[PolyBase, 疑難排解](../../relational-databases/polybase/polybase-troubleshooting.md)|管理 PolyBase 查詢的技術。 使用動態管理檢視 (DMV) 來監視 PolyBase 查詢，並了解如何讀取 PolyBase 查詢計劃來找出效能瓶頸。|  
  
  
