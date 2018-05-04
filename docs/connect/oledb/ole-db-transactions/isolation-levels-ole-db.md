---
title: 隔離等級 (OLE DB) |Microsoft 文件
description: 隔離等級 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 1932e00e3c50e03c7cea5eff876b107df5ddaba0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="isolation-levels-ole-db"></a>隔離等級 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端可以控制連線的交易隔離等級。 若要控制交易隔離等級，會使用 SQL Server 取用者，OLE DB 驅動程式：  
  
-   DBPROPSET_SESSION 屬性 DBPROP_SESS_AUTOCOMMITISOLEVELS OLE DB driver for SQL Server 預設自動認可模式。  
  
     SQL Server 層級的預設值，OLE DB 驅動程式是 DBPROPVAL_TI_READCOMMITTED。  
  
-   *IsoLevel*參數**itransactionlocal:: Starttransaction**本機手動認可交易的方法。  
  
-   *IsoLevel*參數**itransactiondispenser:: Begintransaction**方法適用於 MS DTC 協調分散式交易。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 允許中途讀取隔離等級的唯讀存取。 其他所有等級藉由將鎖定套用至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 物件以限制並行存取。 由於用戶端需要更高的並行存取等級，因此 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會對資料並行存取套用更大的限制。 若要維持資料並行存取的最高層級，SQL Server 取用者，OLE DB 驅動程式應該以智慧方式控制它對特定並行存取等級的要求。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入了快照集隔離等級。 如需詳細資訊，請參閱[使用快照隔離](../../oledb/features/working-with-snapshot-isolation.md)。  
  
## <a name="see-also"></a>另請參閱  
 [交易](../../oledb/ole-db-transactions/transactions.md)  
  
  
