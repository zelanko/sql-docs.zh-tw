---
title: 交易升級 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 893068965ab4566b6f6e4f78e39141de9be2b6ed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855266"
---
# <a name="transaction-promotion"></a>交易升級
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  交易*促銷*說明可以為完全可散發之交易自動升級，視需要的輕量型本機交易。 當 Managed 預存程序在伺服器的資料庫交易內叫用時，Common Language Runtime (CLR) 程式碼會在本機交易的環境中執行。  如果遠端伺服器的連接是在交易資料庫內開啟的，則會將遠端伺服器的連接編列至分散式交易，而且會將本機交易自動升級為分散式交易。 因此，交易升級可以藉由直到需要時才建立分散式交易的方式，將分散式交易的負擔降至最低。 交易升級是自動的如果已使用已啟用**登錄**關鍵字，而且不需要開發人員的介入。 .NET Framework Data Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援交易升級，透過.NET Framework 中的類別處理**System.Data.SqlClient**命名空間。  
  
## <a name="the-enlist-keyword"></a>編列關鍵字  
 **ConnectionString**屬性**SqlConnection**物件支援**登錄**關鍵字，指出是否**System.Data.SqlClient**偵測到交易內容，並自動登記分散式異動中的連接。 如果此關鍵字設定為 True (預設值)，則會在開啟之執行緒的目前交易內容中自動編列連接。 如果此關鍵字設定為 False，則 SqlClient 連接不會與分散式交易進行互動。 如果**登錄**中未指定連接字串，在開啟連接時偵測到，在分散式交易中自動登記連接。  
  
## <a name="distributed-transactions"></a>分散式交易  
 分散式交易通常會消耗大量的系統資源。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 會管理此類交易，並整合在這些交易中存取的所有資源管理員。 交易升級，相反地，是一種特殊形式的**System.Transactions**交易可有效地委派工作給簡單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]交易。 **System.Transactions**， **System.Data.SqlClient**，和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]協調參與處理交易，並視需要將其提升為完全分散式交易的工作。  
  
 使用交易升級的好處是，當連接開啟透過有效**TransactionScope**交易，而沒有其他連接會開啟，將交易認可為輕量型交易，而非會產生完全分散式交易的額外負擔。 如需詳細資訊**TransactionScope**，請參閱[使用 System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合和交易](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
