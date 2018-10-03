---
title: 異動複寫的發行集類型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3943ce65c6984a7ac803b6f5aa657a85acdbd316
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48184098"
---
# <a name="publication-types-for-transactional-replication"></a>異動複寫的發行集類型
  異動複寫提供三種發行集類型：  
  
|發行集類型|描述|  
|----------------------|-----------------|  
|標準交易式發行集|適合於「訂閱者」端的所有資料均為唯讀狀態 (異動複寫並不在「訂閱者」端強制這個屬性) 的拓撲。<br /><br /> 當使用 Transact-SQL 或 Replication Management Objects (RMO) 時，依預設，會建立標準交易式發行集。 當使用「新增發行集精靈」時，它們會透過選取 **[發行集類型]** 頁面上的 **[交易式發行集]** 來建立。<br /><br /> 如需建立發行集的詳細資訊，請參閱 [發行資料和資料庫物件](../publish/publish-data-and-database-objects.md)。|  
|點對點拓撲中的交易式發行集|這個發行集類型的特性為：<br /><br /> 每個位置具有相同的資料，以及同時充當「發行者」與「訂閱者」。<br /><br /> 同一資料行一次僅可以在一個位置變更。<br /><br /> 此拓撲最適合於需要高可用性和讀取延展性的伺服器環境。<br /><br /> <br /><br /> 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [異動複寫](transactional-replication.md)  
  
  
