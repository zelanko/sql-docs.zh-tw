---
title: PolyBase 中的常見問題集 | Microsoft Docs
description: 比較 PolyBase 和連結的伺服器，並比較巨量資料叢集中 PolyBase 和獨立執行個體中的 PolyBase。 了解 PolyBase 2019 的新功能。
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.openlocfilehash: 5083228cc44b859faec866eca7d36aae9626e8fa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760446"
---
# <a name="frequently-asked-questions"></a>常見問題集

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="polybase-vs-linked-servers"></a>PolyBase 與 連結的伺服器
下表強調顯示 PolyBase 和連結的伺服器功能之間的差異：

|PolyBase | 連結的伺服器|
|--------------------------|--------------------------|  
|資料庫範圍物件|執行個體範圍物件|
|使用 ODBC 驅動程式|使用 OLEDB 提供者|
|支援針對所有資料來源的唯讀作業，以及僅針對 HADOOP 與資料集區資料來源的插入作業|同時支援讀取與寫入作業|
|可以向外延展從單一連線對遠端資料來源所進行的查詢 |不可以向外延展從單一連線對遠端資料來源所進行的查詢|
|支援述詞下推|支援述詞下推|
|可用性群組不需要個別設定|可用性群組中的每個執行個體都需要個別設定|
|僅限基本驗證|基本與整合式驗證|
|適用於處理大量資料列的分析查詢|適用於傳回單一或少量資料列的 OLTP 查詢|
|使用外部資料表的查詢無法參與分散式交易|分散式查詢可以參與分散式交易|

## <a name="whats-new-in-polybase-2019"></a>PolyBase 2019 中有哪些新功能？ 

[!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 中的 PolyBase 現在可以從更多不同的資料來源讀取資料。 這些外部資料來源的資料可以儲存為您 SQL Server 上的外部資料表。 PolyBase 也支援下推計算到這些外部資料來源，但不包括 ODBC 泛型型別。

### <a name="compatible-data-sources"></a>相容的資料來源

- SQL Server
- Oracle
- Teradata
- MongoDB
- 相容的 ODBC 泛型型別
  
> [!NOTE]
> PolyBase 可讓您使用協力廠商 ODBC 驅動程式連線到外部資料來源。 這些驅動程式並未隨附於 PolyBase，且可能不會如預期般運作。 如需詳細資訊，請瀏覽我們的[指南](../../relational-databases/polybase/polybase-configure-odbc-generic.md)以取得 PolyBase ODBC 一般設定。  

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>巨量資料叢集中的 PolyBase 與獨立執行個體中的 PolyBase

下表強調顯示於 [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 獨立安裝及 [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 巨量資料叢集中所提供的 PolyBase 功能：

|功能 |巨量資料叢集|獨立執行個體|
|--------------------------|--------------------------|---------|   
|針對 SQL Server、Oracle、Teradata 和 Mongo DB 建立外部資料來源 |X|X |
|使用相容的協力廠商 ODBC 驅動程式建立外部資料來源 | | X|
|針對 HADOOP 資料來源建立外部資料來源 | X| X|
|針對 Azure Blob 儲存體建立外部資料來源 | X| X|
|在 SQL Server 資料集區上建立外部資料表 | X| |
|在 SQL Server 存放集區上建立外部資料表 | X| |
|向外延展查詢執行 | X| X|

> [!NOTE]
>此表格並未描述最新 [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] CTP 中所提供的功能。 針對這些可用功能，請參閱版本資訊。 如需使用 ODBC 一般連接器之連線的詳細資訊，請瀏覽我們的[設定 ODBC 泛型型別的操作指南](polybase-configure-odbc-generic.md)。