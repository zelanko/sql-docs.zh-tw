---
title: 異動複寫的發行集類型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactional replication, publications
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 11e9e6ffafe62c66684470b4b04e2e0b67cc868b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030015"
---
# <a name="publication-types-for-transactional-replication"></a>異動複寫的發行集類型
  異動複寫提供三種發行集類型：  
  
|發行集類型|描述|  
|----------------------|-----------------|  
|標準交易式發行集|適合於「訂閱者」端的所有資料均為唯讀狀態 (異動複寫並不在「訂閱者」端強制這個屬性) 的拓撲。<br /><br /> 當使用 Transact-SQL 或 Replication Management Objects (RMO) 時，依預設，會建立標準交易式發行集。 當使用「新增發行集精靈」時，它們會透過選取 **[發行集類型]** 頁面上的 **[交易式發行集]** 來建立。<br /><br /> 如需建立發行集的詳細資訊，請參閱 [發行資料和資料庫物件](../publish/publish-data-and-database-objects.md)。|  
|點對點拓撲中的交易式發行集|這個發行集類型的特性為：<br /><br /> 每個位置具有相同的資料，以及同時充當「發行者」與「訂閱者」。<br /><br /> 同一資料行一次僅可以在一個位置變更。<br /><br /> 此拓撲最適合於需要高可用性和讀取延展性的伺服器環境。<br /><br /> <br /><br /> 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [異動複寫](transactional-replication.md)  
  
  