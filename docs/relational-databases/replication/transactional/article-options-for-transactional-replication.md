---
title: 異動複寫的發行項選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
caps.latest.revision: 30
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ae80de532c6cddf4e67b4e8161ea6219beb88f10
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349190"
---
# <a name="article-options-for-transactional-replication"></a>異動複寫的發行項選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  針對交易式發行集中的發行項提供了一些選項。 使用異動複寫，您可以執行下列項目：  
  
-   指定變更從「發行者」傳播到「訂閱者」的方式。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
-   指定複寫預存程序的執行。 針對會影響大量資料的維護導向預存程序複寫結果時很有用。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
-   指定結構描述選項，如條件約束和觸發程序是否複製到訂閱者。 如需詳細資訊，請參閱 [指定結構描述選項](../../../relational-databases/replication/publish/specify-schema-options.md)。  
  
-   使用資料列篩選與資料行篩選。 篩選資料表發行項可讓您建立即將發行的資料分割。 如需詳細資訊，請參閱[篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
