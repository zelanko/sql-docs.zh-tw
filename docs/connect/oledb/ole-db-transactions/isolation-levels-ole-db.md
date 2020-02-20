---
title: 隔離等級 (OLE DB) | Microsoft Docs
description: 隔離等級 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2c9f3a7cd06f801555ab373e7e54fbf1b620d894
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993969"
---
# <a name="isolation-levels-ole-db"></a>隔離等級 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端可以控制連線的交易隔離等級。 若要控制交易隔離等級，OLE DB Driver for SQL Server 取用者會使用：  
  
-   適用於 OLE DB Driver for SQL Server 預設自動認可模式的 DBPROPSET_SESSION 屬性 DBPROP_SESS_AUTOCOMMITISOLEVELS。  
  
     等級的 OLE DB Driver for SQL Server 預設值是 DBPROPVAL_TI_READCOMMITTED。  
  
-   適用於本機手動認可交易之 **ITransactionLocal::StartTransaction** 方法的 *isoLevel* 參數。  
  
-   適用於 MS DTC 協調分散式交易之 **ITransactionDispenser::BeginTransaction** 方法的 *isoLevel* 參數。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 允許中途讀取隔離等級的唯讀存取。 其他所有等級藉由將鎖定套用至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 物件以限制並行存取。 由於用戶端需要更高的並行存取等級，因此 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會對資料並行存取套用更大的限制。 若要維持資料並行存取的最高等級，OLE DB Driver for SQL Server 取用者應該以智慧方式控制它對特定並行存取等級的要求。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入了快照集隔離等級。 如需詳細資訊，請參閱[使用快照隔離](../../oledb/features/working-with-snapshot-isolation.md)。  
  
## <a name="see-also"></a>另請參閱  
 [交易](../../oledb/ole-db-transactions/transactions.md)  
  
  
