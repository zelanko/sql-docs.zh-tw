---
title: 交易促銷 |微軟文件
description: 在 SQL Server CLR 整合中,可以通過事務升級將輕量級本地事務提升為完全可分配事務。
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
ms.openlocfilehash: e77409f6bf6c71363e030f29f86f41205dd4a0f0
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487466"
---
# <a name="transaction-promotion"></a>交易升級
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  事務*升級*描述一個輕量級的本地事務,可以根據需要自動提升為完全可分配事務。 當 Managed 預存程序在伺服器的資料庫交易內叫用時，Common Language Runtime (CLR) 程式碼會在本機交易的環境中執行。  如果遠端伺服器的連接是在交易資料庫內開啟的，則會將遠端伺服器的連接編列至分散式交易，而且會將本機交易自動升級為分散式交易。 因此，交易升級可以藉由直到需要時才建立分散式交易的方式，將分散式交易的負擔降至最低。 事務升級是自動的,如果已使用**Enlist**關鍵字啟用,並且不需要開發人員的干預。 .NET 框架數據提供程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用於 支援事務升級,通過 .NET 框架**系統中的**類進行處理。  
  
## <a name="the-enlist-keyword"></a>編列關鍵字  
 **SqlConnection**物件的**ConnectString**屬性支援**Enlist**關鍵字,該關鍵字指示**System.Data.SqlClient**是否檢測事務上下文並自動在分散式事務中登記連接。 如果此關鍵字設定為 True (預設值)，則會在開啟之執行緒的目前交易內容中自動編列連接。 如果此關鍵字設定為 False，則 SqlClient 連接不會與分散式交易進行互動。 如果在連接字串中未指定**Enlist,** 則如果在打開連接時偵測到連接,則連接將自動登記在分散式事務中。  
  
## <a name="distributed-transactions"></a>分散式交易  
 分散式交易通常會消耗大量的系統資源。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 會管理此類交易，並整合在這些交易中存取的所有資源管理員。 另一方面,事務促進是一種特殊形式的**系統。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **系統.事務**,**系統.Data.SqlClient,** 並[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]協調處理事務所涉及的工作,根據需要將其提升為完全分散式事務。  
  
 使用事務升級的好處是,當與活動**事務範圍**事務打開連接,並且未打開任何其他連接時,事務將作為羽量級事務提交,而不是產生完全分散式事務的額外開銷。 有關**事務範圍**的詳細資訊,請參閱[使用系統。](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合和交易](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
