---
title: PolyBase 中的常見問題集 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: ''
ms.openlocfilehash: 331ac177831b1e07cfab253c363a35f2bab42a6c
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072874"
---
# <a name="frequently-asked-questions"></a>常見問題集

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>巨量資料叢集中的 PolyBase 與 獨立執行個體中的 PolyBase

|功能 |巨量資料叢集| 獨立執行個體|
|--------------------------|--------------------------|---------|   
|建立外部資料表| X| X|
|從 SQL Server、Oracle、Teradata 和 Mongo DB 建立外部資料來源 |X|X |
|使用相容的協力廠商 ODBC 驅動程式建立外部資料來源 | | X|
|PolyBase 向外延展群組 | X | |
|資料集區執行個體 | X| |
|存放集區執行個體| X| |

>[!NOTE]
>
>如需使用一般 ODBC 連接器進行連線的詳細資訊，請瀏覽我們的[設定 ODBC 泛型型別的操作指南](polybase-configure-odbc-generic.md)

## <a name="whats-new-with-polybase-in-sql-server-2019"></a>SQL Server 2019 中的 PolyBase 有哪些新功能？ 

SQL Server 2019 中的 PolyBase 現在可以從更多不同的資料來源讀取資料。 這些外部資料來源的資料可以儲存為您 SQL Server 上的外部資料表。 PolyBase 也支援下推計算到這些外部資料來源，但不包括 ODBC 泛型型別。 

### <a name="compatible-data-sources"></a>相容的資料來源

- [SQL Server]
- Oracle
- Teradata
- MongoDB
- **相容的** ODBC 泛型型別

  > [!NOTE]
  >
  >PolyBase 可讓您使用協力廠商 ODBC 驅動程式連線到外部資料來源。 這些驅動程式並未隨附於 PolyBase，且可能會如預期般運作。 如需詳細資訊，請瀏覽我們的[指南](polybase-configure-odbc-generic.md)以了解一般 PolyBase ODBC 設定。  

## <a name="polybase-vs-linked-servers"></a>PolyBase 與 連結的伺服器

|PolyBase | 連結的伺服器|
|--------------------------|--------------------------|  
|資料庫範圍物件|執行個體範圍物件| 
|使用 ODBC 驅動程式|使用 OLEDB 提供者| 
| 僅支援唯讀作業。 未來將會擴充| 僅支援唯讀作業。 未來將會擴充| 
|查詢可向外延展並支援下推|查詢是單一執行緒並支援下推|
|Always On 可用性群組不需要個別設定|Always On 可用性群組中的每個執行個體需要個別設定|
|僅限基本驗證。 SQL Server 2019 中將改善|基本與整合式驗證|