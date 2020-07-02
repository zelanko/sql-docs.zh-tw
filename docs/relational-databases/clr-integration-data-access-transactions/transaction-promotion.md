---
title: 交易升級 |Microsoft Docs
description: 在 SQL Server CLR 整合中，輕量的本機交易可以透過交易升級升級為完全可散發的交易。
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
ms.openlocfilehash: 1267a916e1f3ed9bbcdf3e03240f5fcc39b7eb1b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765353"
---
# <a name="transaction-promotion"></a>交易升級
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  交易*升級*描述輕量的本機交易，可以視需要自動升級為完全可散發的交易。 當 Managed 預存程序在伺服器的資料庫交易內叫用時，Common Language Runtime (CLR) 程式碼會在本機交易的環境中執行。  如果遠端伺服器的連接是在交易資料庫內開啟的，則會將遠端伺服器的連接編列至分散式交易，而且會將本機交易自動升級為分散式交易。 因此，交易升級可以藉由直到需要時才建立分散式交易的方式，將分散式交易的負擔降至最低。 交易升級是自動的，如果已使用**登錄關鍵字啟用**，則不需要開發人員介入。 的 .NET Framework Data Provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可提供交易升級的支援，並透過 .NET Framework **SqlClient**命名空間中的類別來處理。  
  
## <a name="the-enlist-keyword"></a>編列關鍵字  
 **SqlConnection**物件的**ConnectionString**屬性支援**登錄關鍵字，** 這會指出**SqlClient**是否偵測到交易內容，並自動在分散式交易中登記連接。 如果此關鍵字設定為 True (預設值)，則會在開啟之執行緒的目前交易內容中自動編列連接。 如果此關鍵字設定為 False，則 SqlClient 連接不會與分散式交易進行互動。 如果在連接字串中未指定登錄 **，當連接**開啟時，連接會自動登記在分散式交易中。  
  
## <a name="distributed-transactions"></a>分散式交易  
 分散式交易通常會消耗大量的系統資源。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 會管理此類交易，並整合在這些交易中存取的所有資源管理員。 另一方面，交易升級是系統的特殊形式 **。交易**交易可有效地將工作委派給簡單的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易。 **SqlClient** **，並** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 協調處理交易時所涉及的工作，並視需要將它升級為完整的分散式交易。  
  
 使用交易升級的優點是，當使用作用中的**TransactionScope**交易開啟連接，且未開啟其他連接時，交易會認可為輕量交易，而不會產生完整分散式交易的額外負擔。 如需**TransactionScope**的詳細資訊，請參閱[使用 System. 交易](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合和交易](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
