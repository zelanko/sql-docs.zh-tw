---
title: CLR 整合和交易 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9cab6c061f8baac232563b4afe41952da1b4892e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921553"
---
# <a name="clr-integration-and-transactions"></a>CLR 整合和交易
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **System.Transactions**命名空間提供與 ADO.NET 完全整合的交易架構和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]common language runtime (CLR) 整合。 **System.Transactions**和 ADO.NET 一起運作，以擴充和簡化本機和分散式交易在 managed 應用程式使用。  
  
> [!NOTE]  
>  CLR 使用者定義程序 (UDP) 不能與執行所在的同一台伺服器建立連接 (回送連接)，也不能編列在相同的交易中。 如果嘗試這麼做，系統就會封鎖連接嘗試，而控制權將不會傳回給 UDP。 這樣將導致 UDP 上產生逾時錯誤 (訊息 1206)。  
  
 如需有關交易和 .NET Framework 的詳細資訊，請參閱 .NET Framework SDK 中的＜執行交易＞和＜利用交易＞。  
  
## <a name="in-this-section"></a>本節內容  
 [交易升級](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 描述升級交易的功能，以及如何使用這項功能。  
  
 [存取目前交易](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 描述如何存取目前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上於同處理序 (In-Process) 中執行的交易。  
  
 [使用 System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 描述如何使用**System.Transactions**應用程式開發介面 (API)，在受管理的應用程式中。  
  
 [交易存留期間](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 描述在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中所啟動的交易和在 CLR 應用程式中所啟動的交易在存留期間上的差異。  
  
## <a name="see-also"></a>另請參閱  
 [從 CLR 資料庫物件進行資料存取](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
