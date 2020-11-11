---
title: CLR 整合和交易 |Microsoft Docs
description: 針對 CLR 整合和交易，系統交易和 ADO.NET 會一起運作，以擴充和簡化在 managed 應用程式中使用本機和分散式交易的方式。
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
ms.openlocfilehash: bd65fce2f2a2bdf2ce25f4811063f7f9d56d2e15
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521129"
---
# <a name="clr-integration-and-transactions"></a>CLR 整合和交易
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  System.string **命名空間提供的交易架構** ，與 ADO.NET 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] common LANGUAGE runtime (CLR) 整合完全整合。 System.string 和 ADO.NET 會一起運作，以擴充和簡化在受控應用程式中使用本機和分散式交易的 **方式。**  
  
> [!NOTE]  
>  CLR 使用者定義程序 (UDP) 不能與執行所在的同一台伺服器建立連接 (回送連接)，也不能編列在相同的交易中。 如果嘗試這麼做，系統就會封鎖連接嘗試，而控制權將不會傳回給 UDP。 這樣將導致 UDP 上產生逾時錯誤 (訊息 1206)。  
  
 如需有關交易和 .NET Framework 的詳細資訊，請參閱 .NET Framework SDK 中的＜執行交易＞和＜利用交易＞。  
  
## <a name="in-this-section"></a>本節內容  
 [交易升級](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 描述升級交易的功能，以及如何使用這項功能。  
  
 [存取目前交易](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 描述如何存取目前在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上於同處理序 (In-Process) 中執行的交易。  
  
 [使用 System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 描述如何在您的受控應用程式中使用 (API) 的「 **系統交易** 」應用程式設計介面。  
  
 [交易存留期間](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 描述在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中所啟動的交易和在 CLR 應用程式中所啟動的交易在存留期間上的差異。  
  
## <a name="see-also"></a>另請參閱  
 [從 CLR 資料庫物件進行資料存取](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
