---
description: " (Native Client OLE DB 提供者的隔離等級) "
title: " (Native Client OLE DB provider) 的隔離等級 |Microsoft Docs"
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6517d7a49aee24cedb22b037d373d0d56598af54
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97418671"
---
# <a name="isolation-levels-native-client-ole-db-provider"></a> (Native Client OLE DB 提供者的隔離等級) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端可以控制連線的交易隔離等級。 若要控制交易隔離等級， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者取用者會使用：  
  
-   DBPROPSET_SESSION DBPROP_SESS_AUTOCOMMITISOLEVELS [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者預設自動認可模式的屬性。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]層級的原生用戶端 OLE DB 提供者預設為 DBPROPVAL_TI_READCOMMITTED。  
  
-   適用於本機手動認可交易之 **ITransactionLocal::StartTransaction** 方法的 *isoLevel* 參數。  
  
-   適用於 MS DTC 協調分散式交易之 **ITransactionDispenser::BeginTransaction** 方法的 *isoLevel* 參數。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許中途讀取隔離等級的唯讀存取。 其他所有等級藉由將鎖定套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件以限制並行存取。 由於用戶端需要更高的並行存取等級，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會對資料並行存取套用更大的限制。 若要維持資料平行存取的最高層級， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者取用者應該以智慧方式控制其對特定平行存取層級的要求。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 引入了快照集隔離等級。 如需詳細資訊，請參閱[使用快照隔離](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)。  
  
## <a name="see-also"></a>另請參閱  
 [交易](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
