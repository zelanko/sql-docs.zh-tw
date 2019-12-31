---
title: 設定 PolyBase 連線能力
description: 說明如何在平行處理資料倉儲中設定 PolyBase，以連接到外部 Hadoop 或 Microsoft Azure 儲存體 blob 資料來源。 使用 PolyBase 執行查詢，以整合來自多個來源的資料，包括 Hadoop、Azure blob 儲存體和平行處理資料倉儲。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3b754fb2de33a230bc7d27f239b2778d2849fd5a
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401269"
---
# <a name="what-is-polybase"></a>什麼是 PolyBase？
PolyBase 可讓您的分析平臺系統（AP）處理可讀取資料，並將資料寫入外部資料源的 Transact-SQL 查詢。 存取外部資料的相同查詢也可以包含您的 AP 中的關聯資料表。 這可讓您將來自外部來源的資料與您的 AP 資料庫中的高價值關聯式資料結合。

![PolyBase 邏輯](media/polybase/polybase-logical.png)

AP 上的 PolyBase 支援讀取和寫入 Hadoop （HDFS）檔案系統和 Azure Blob 儲存體。 PolyBase 也能夠將一些計算推送至 Hadoop 節點做為 mapreduce 工作，以優化整體查詢效能。 AP 上的 PolyBase 可以在分隔的文字、ORC 和 Parquet 檔案上運作。 如需完整描述和其功能，請參閱[什麼是 PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) 。

> [!NOTE]
> AP 目前僅支援標準一般用途 v1 本機冗余（LRS） Azure Blob 儲存體。

## <a name="features-and-limitations"></a>功能和限制
請參閱[功能和限制](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary)，以取得 PolyBase 功能的摘要，以及 ap 和其他 SQL Server 產品的已知限制。

> [!NOTE] 
> 其他 PolyBase 相關文章將描述如何在 AP 2016 （AU6）和更新版本上設定 PolyBase。

## <a name="see-also"></a>另請參閱
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob 儲存體](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
