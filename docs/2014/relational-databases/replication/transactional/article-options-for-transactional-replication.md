---
title: 異動複寫的發行項選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
caps.latest.revision: 29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9be81144ab7d2653a050ce36f06bd16211a589cd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270514"
---
# <a name="article-options-for-transactional-replication"></a>異動複寫的發行項選項
  針對交易式發行集中的發行項提供了一些選項。 使用異動複寫，您可以執行下列項目：  
  
-   指定變更從「發行者」傳播到「訂閱者」的方式。 如需詳細資訊，請參閱[指定交易式發行項變更的傳播方式](transactional-articles-specify-how-changes-are-propagated.md)。  
  
-   指定複寫預存程序的執行。 針對會影響大量資料的維護導向預存程序複寫結果時很有用。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
-   指定結構描述選項，如條件約束和觸發程序是否複製到訂閱者。 如需詳細資訊，請參閱 [指定結構描述選項](../publish/specify-schema-options.md)。  
  
-   使用資料列篩選與資料行篩選。 篩選資料表發行項可讓您建立即將發行的資料分割。 如需詳細資訊，請參閱[篩選發行的資料](../publish/filter-published-data.md)。  
  
## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](../publish/publish-data-and-database-objects.md)  
  
  
