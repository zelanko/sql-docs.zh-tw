---
title: 訂閱，未散發的命令 (交易式訂閱) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 8047bc8ec2789c1b47eb4525c0576d46f11a1248
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39546308"
---
# <a name="subscription-undistributed-commands-transactional-subscription"></a>訂閱，未散發的命令 (交易式訂閱)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **[未散發的命令]** 索引標籤會顯示散發資料庫中尚未傳遞給選取之訂閱者的命令數目，以及傳遞這些命令的估計時間等相關資訊。 如需在散發資料庫中檢視命令的資訊，請參閱 [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)。  
  
## <a name="options"></a>選項。  
 **在散發資料庫中，等候要套用到此訂閱者的命令數目**  
 散發資料庫中尚未傳遞給選取之訂閱者的命令數目。 由一個 Transact-SQL 資料操作語言 (DML) 陳述式或一個資料定義語言 (DDL) 陳述式組成的命令。  
  
 **依據過去的效能，估計套用這些命令的時間**  
 估計將命令傳遞給訂閱者所需的時間量。 如果此值大於產生快照集並將其套用至訂閱者所需的時間量，則請考慮重新初始化訂閱者。 如需詳細資訊，請參閱 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
