---
title: 交易 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dca9b7a3289390b1d1e20e1b0d18c23b44b87617
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213897"
---
# <a name="transactions"></a>交易
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會實作本機交易支援。 取用者可以使用 Microsoft 分散式交易協調器 (MS DTC) 來使用分散式或協調的交易。 取用者需要跨多個工作階段的交易控制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者可以聯結起始和維護的 MS DTC 交易。  
  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會使用自動認可交易模式，其中每個離散的動作，在取用者工作階段上包含完整的交易執行個體的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者自動認可模式為本機，而自動認可交易絕不會跨越多個單一工作階段。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**ITransactionLocal**介面，讓取用者明確地使用並隱含地啟動的執行個體的單一連接中的 交易[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者不支援巢狀本機交易。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [支援本機交易](supporting-local-transactions.md)  
  
-   [支援分散式交易](supporting-distributed-transactions.md)  
  
-   [隔離層級&#40;OLE DB&#41;](isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
