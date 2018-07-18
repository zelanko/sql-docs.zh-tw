---
title: 交易 |Microsoft 文件
description: SQL Server OLE DB 驅動程式中的交易
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 1f1e0b252960468e443b157c7c95213809a4d318
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689311"
---
# <a name="transactions"></a>交易
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server OLE DB 驅動程式會實作本機交易支援。 取用者可以使用 Microsoft 分散式交易協調器 (MS DTC) 來使用分散式或協調的交易。 取用者需要跨多個工作階段的交易控制，SQL Server OLE DB 驅動程式可以聯結起始和維護的 MS DTC 交易。  
  
 根據預設，SQL Server OLE DB 驅動程式會使用自動認可交易模式，其中每個離散的動作，取用者工作階段上包含完整的交易執行個體的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 SQL Server 自動認可模式，OLE DB 驅動程式為本機，而自動認可交易絕不會跨越多個單一工作階段。  
  
 SQL Server OLE DB 驅動程式會公開**ITransactionLocal**介面，讓取用者明確地使用並隱含地啟動交易的執行個體的單一連接上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 SQL Server OLE DB 驅動程式不支援巢狀本機交易。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [支援本機交易](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [支援分散式交易](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [隔離等級&#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
