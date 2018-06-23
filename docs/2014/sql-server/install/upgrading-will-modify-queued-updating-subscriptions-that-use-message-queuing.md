---
title: 升級將修改使用 Message Queuing 的佇列更新訂閱 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication]
- MSMQ [SQL Server replication]
- queues [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
ms.assetid: 97944de3-fbad-4db1-939a-dcd550bf5893
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: efb1b244385061bee985ec04b5f90d3fb349aef3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030425"
---
# <a name="upgrading-will-modify-queued-updating-subscriptions-that-use-message-queuing"></a>升級將會修改使用 Message Queuing 的佇列更新訂閱
  Upgrade Advisor 偵測到您可能有一或多個使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (也稱為 MSMQ) 的佇列更新訂閱。 複寫不再支援訊息佇列，因此將會修改訂閱以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列。  
  
 值**sql**允許。 在升級期間，系統會將使用訊息佇列的現有發行集修改為使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列。 如果您有應用程式是依賴使用 Message Queuing 的佇列更新，這些應用程式都需要重寫，以配合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列。 如需有關佇列更新訂閱的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜異動複寫的可更新訂閱＞。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在升級時，如果 Message Queuing 服務正在執行，升級會移除現有的 Message Queuing 訂閱佇列。  
  
 如果 Message Queuing 服務未在執行中，請在升級完成後手動移除佇列。 如需有關如何移除佇列的詳細資訊，請參閱 Windows 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [複寫升級問題](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  