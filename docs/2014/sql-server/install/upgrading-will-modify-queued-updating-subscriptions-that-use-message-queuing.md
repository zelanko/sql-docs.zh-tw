---
title: 升級將修改使用 Message Queuing 的佇列更新訂閱 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication]
- MSMQ [SQL Server replication]
- queues [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
ms.assetid: 97944de3-fbad-4db1-939a-dcd550bf5893
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c723050f9e860534c5298df9a487337e319ff91
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091406"
---
# <a name="upgrading-will-modify-queued-updating-subscriptions-that-use-message-queuing"></a>升級將會修改使用 Message Queuing 的佇列更新訂閱
  Upgrade Advisor 偵測到您可能有一或多個使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (也稱為 MSMQ) 的佇列更新訂閱。 複寫不再支援訊息佇列，因此將會修改訂閱以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列。  
  
 值**sql**允許。 在升級期間，系統會將使用訊息佇列的現有發行集修改為使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列。 如果您有應用程式是依賴使用 Message Queuing 的佇列更新，這些應用程式都需要重寫，以配合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 佇列。 如需有關佇列更新訂閱的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜異動複寫的可更新訂閱＞。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在升級時，如果 Message Queuing 服務正在執行，升級會移除現有的 Message Queuing 訂閱佇列。  
  
 如果 Message Queuing 服務未在執行中，請在升級完成後手動移除佇列。 如需有關如何移除佇列的詳細資訊，請參閱 Windows 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [複寫升級問題](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
