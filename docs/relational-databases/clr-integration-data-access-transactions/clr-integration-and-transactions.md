---
title: CLR 整合和事務 |微軟文件
description: System.事務命名空間提供了一個與ADO.NET和 SQL Server CLR 整合完全整合的事務框架。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d7e4ac0e338ac556c88c8cc22d6a87a53c67d51
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487473"
---
# <a name="clr-integration-and-transactions"></a>CLR 整合和交易
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **System.事務**命名空間提供了一個事務框架,該框架與ADO.NET[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 通用語言運行時 (CLR) 整合完全整合。 **系統.事務**和ADO.NET協同工作,以擴展和簡化託管應用程式中本地和分散式事務的使用。  
  
> [!NOTE]  
>  CLR 使用者定義程序 (UDP) 不能與執行所在的同一台伺服器建立連接 (回送連接)，也不能編列在相同的交易中。 如果嘗試這麼做，系統就會封鎖連接嘗試，而控制權將不會傳回給 UDP。 這樣將導致 UDP 上產生逾時錯誤 (訊息 1206)。  
  
 如需有關交易和 .NET Framework 的詳細資訊，請參閱 .NET Framework SDK 中的＜執行交易＞和＜利用交易＞。  
  
## <a name="in-this-section"></a>本節內容  
 [交易升級](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 描述升級交易的功能，以及如何使用這項功能。  
  
 [存取目前交易](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 描述如何存取目前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上於同處理序 (In-Process) 中執行的交易。  
  
 [使用 System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 描述如何在託管應用程式中使用**System.事務**應用程式程式設計介面 (API)。  
  
 [交易存留期間](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 描述在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中所啟動的交易和在 CLR 應用程式中所啟動的交易在存留期間上的差異。  
  
## <a name="see-also"></a>另請參閱  
 [從 CLR 資料庫物件進行資料存取](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
