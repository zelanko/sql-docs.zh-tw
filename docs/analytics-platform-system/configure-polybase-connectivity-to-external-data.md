---
title: 設定 PolyBase 連線能力-Analytics Platform System |Microsoft Docs
description: 說明如何設定連接至外部 Hadoop 或 Microsoft Azure 儲存體 blob 資料來源的平行處理資料倉儲的 PolyBase。 若要執行查詢來整合資料的多個來源，包括 Hadoop、 Azure blob 儲存體和平行處理資料倉儲使用 PolyBase。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: da6d71521f72ff23b4caf2f27dbc663dee684592
ms.sourcegitcommit: 5afec8b4b73ce1727e4e5cf875d1e1ce9df50eab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/28/2018
ms.locfileid: "47450293"
---
# <a name="what-is-polybase"></a>PolyBase 是什麼？
PolyBase 可讓您的 「 Analytics Platform System (APS) 」，來處理 TRANSACT-SQL 查詢，可以從中讀取資料，並將資料寫入外部資料來源。 存取外部資料的相同查詢也可以包含您 AP 關聯資料表。 這可讓您結合來自外部來源的資料高價值 AP 資料庫中的關聯式資料。

![PolyBase 邏輯](media/polybase/polybase-logical.png)

AP 上的 PolyBase 支援讀取和寫入至 Hadoop (HDFS) 檔案系統和 Azure Blob 儲存體。 PolyBase 也能夠將一些計算推送到 Hadoop 節點中，為 mapreduce 工作，以最佳化整體查詢效能。 AP 上的 PolyBase 可處理分隔的文字、 ORC 和 Parquet 檔案。 請參閱[什麼是 PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)完整的描述和其功能。

> [!NOTE]
> APS 目前僅支援標準的一般用途 v1 本地備援 (LRS) Azure Blob 儲存體。

## <a name="features-and-limitations"></a>功能和限制
請參閱[功能和限制](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary)的摘要的 PolyBase 功能 AP 和其他 SQL Server 產品的可用且已知限制。

> [!NOTE] 
> PolyBase 的其餘部分的相關文章將描述如何設定 PolyBase APS 2016 (AU6) 和更新版本。

## <a name="see-also"></a>另請參閱
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob 儲存體](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
