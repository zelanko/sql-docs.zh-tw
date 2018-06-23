---
title: CLR 整合和交易 |Microsoft 文件
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b82456883db306009f4d2027c1cd7f91ff985f85
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034154"
---
# <a name="clr-integration-and-transactions"></a>CLR 整合和交易
  `System.Transactions` 命名空間會提供與 ADO.NET 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Common Language Runtime (CLR) 整合完全整合的交易架構。 `System.Transactions` 和 ADO.NET 能搭配使用，以擴充並簡化本機和分散式交易在 Managed 應用程式中的使用。  
  
> [!NOTE]  
>  CLR 使用者定義程序 (UDP) 不能與執行所在的同一台伺服器建立連接 (回送連接)，也不能編列在相同的交易中。 如果嘗試這麼做，系統就會封鎖連接嘗試，而控制權將不會傳回給 UDP。 這樣將導致 UDP 上產生逾時錯誤 (訊息 1206)。  
  
 如需有關交易和 .NET Framework 的詳細資訊，請參閱 .NET Framework SDK 中的＜執行交易＞和＜利用交易＞。  
  
## <a name="in-this-section"></a>本節內容  
 [交易升級](transaction-promotion.md)  
 描述升級交易的功能，以及如何使用這項功能。  
  
 [存取目前交易](accessing-the-current-transaction.md)  
 描述如何存取目前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上於同處理序 (In-Process) 中執行的交易。  
  
 [使用 System.Transactions](../native-client-ole-db-transactions/transactions.md)  
 描述如何在 Managed 應用程式中使用 `System.Transactions` 應用程式開發介面 (API)。  
  
 [交易存留期間](transaction-lifetimes.md)  
 描述在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中所啟動的交易和在 CLR 應用程式中所啟動的交易在存留期間上的差異。  
  
## <a name="see-also"></a>另請參閱  
 [從 CLR 資料庫物件進行資料存取](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  