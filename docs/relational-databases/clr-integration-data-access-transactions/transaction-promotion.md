---
title: "交易升級 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: baf9282b5afc062c91ade5ee4c4bbe8d9d1485bf
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="transaction-promotion"></a>交易升級
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
交易*升級*描述可以自動提升為完全可散發交易視的輕量型本機交易。 當 Managed 預存程序在伺服器的資料庫交易內叫用時，Common Language Runtime (CLR) 程式碼會在本機交易的環境中執行。  如果遠端伺服器的連接是在交易資料庫內開啟的，則會將遠端伺服器的連接編列至分散式交易，而且會將本機交易自動升級為分散式交易。 因此，交易升級可以藉由直到需要時才建立分散式交易的方式，將分散式交易的負擔降至最低。 交易升級是自動的如果它已啟用使用**登錄**關鍵字，而且不需要開發人員的介入。 .NET Framework Data Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供支援交易升級，透過.NET Framework 中的類別處理**System.Data.SqlClient**命名空間。  
  
## <a name="the-enlist-keyword"></a>編列關鍵字  
 **ConnectionString**屬性**SqlConnection**物件支援**登錄**關鍵字，指出是否**System.Data.SqlClient**偵測到異動內容，自動登記分散式交易中的連接。 如果此關鍵字設定為 True (預設值)，則會在開啟之執行緒的目前交易內容中自動編列連接。 如果此關鍵字設定為 False，則 SqlClient 連接不會與分散式交易進行互動。 如果**登錄**中未指定連接字串中，開啟連接時偵測到，在分散式交易中自動登記連接。  
  
## <a name="distributed-transactions"></a>分散式交易  
 分散式交易通常會消耗大量的系統資源。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 會管理此類交易，並整合在這些交易中存取的所有資源管理員。 交易升級，相反地，是一種特殊形式**System.Transactions**有效地委派工作給簡單的交易[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]交易。 **System.Transactions**， **System.Data.SqlClient**，和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]協調處理交易，並視需要將其提升為完全分散式交易時所涉及的工作。  
  
 使用交易升級的好處是： 當以作用中開啟連接**TransactionScope**交易，而沒有其他連接開啟開啟時，將交易認可為輕量型交易，而非產生完全分散式異動的額外負擔。 如需有關**TransactionScope**，請參閱[使用 System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合和交易](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
