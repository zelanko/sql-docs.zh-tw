---
title: 交易升級 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bf30b06849c0384d118edf635a6361712c2d22f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874764"
---
# <a name="transaction-promotion"></a>交易升級
  交易*促銷*說明可以為完全可散發之交易自動升級，視需要的輕量型本機交易。 當 Managed 預存程序在伺服器的資料庫交易內叫用時，Common Language Runtime (CLR) 程式碼會在本機交易的環境中執行。  如果遠端伺服器的連接是在交易資料庫內開啟的，則會將遠端伺服器的連接編列至分散式交易，而且會將本機交易自動升級為分散式交易。 因此，交易升級可以藉由直到需要時才建立分散式交易的方式，將分散式交易的負擔降至最低。 如果您已經使用 `Enlist` 關鍵字啟用交易升級，則交易升級是自動的，無需開發人員從中操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 .NET Framework 資料提供者支援交易升級，可透過 .NET Framework `System.Data.SqlClient` 命名空間中的類別來處理。  
  
## <a name="the-enlist-keyword"></a>編列關鍵字  
 `ConnectionString` 物件的 `SqlConnection` 屬性支援 `Enlist` 關鍵字，它表示 `System.Data.SqlClient` 是否會偵測到交易內容，並自動在分散式交易中編列連接。 如果此關鍵字設定為 True (預設值)，則會在開啟之執行緒的目前交易內容中自動編列連接。 如果此關鍵字設定為 False，則 SqlClient 連接不會與分散式交易進行互動。 如果未在連接字串中指定 `Enlist`，則若在開啟連接時偵測到連接，便會自動在分散式交易中編列該連接。  
  
## <a name="distributed-transactions"></a>分散式交易  
 分散式交易通常會消耗大量的系統資源。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 會管理此類交易，並整合在這些交易中存取的所有資源管理員。 另一方面，交易升級是 `System.Transactions` 交易的特殊形式，可有效地委派工作給簡單的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易。 `System.Transactions`、`System.Data.SqlClient` 及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會協調處理交易時所涉及的工作，並視需要將其提升為完全分散式交易。  
  
 使用交易升級的好處是：當以作用中的 `TransactionScope` 交易開啟連接，且未開啟其他連接時，會將交易認可為輕量型交易，不會產生完全分散式交易的額外負擔。 如需詳細資訊`TransactionScope`，請參閱 <<c2> [ 使用 System.Transactions](../native-client-ole-db-transactions/transactions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合和交易](clr-integration-and-transactions.md)  
  
  
