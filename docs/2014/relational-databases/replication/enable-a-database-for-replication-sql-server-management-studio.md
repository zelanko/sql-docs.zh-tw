---
title: 為複寫啟用資料庫 (SQL Server Management Studio) | Microsoft Docs
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
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3c6a7a83720611d48a47d92467320618565e26af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034114"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>為複寫啟用資料庫 (SQL Server Management Studio)
  **sysadmin** 固定伺服器角色成員使用「新增發行集精靈」建立發行集時，會為複寫隱含啟用資料庫。 **sysadmin** 固定伺服器角色成員同樣可以為複寫明確啟用資料庫，以便 **db_owner** 固定資料庫角色成員可以在該資料庫中建立一個或多個發行集。 若要明確啟用資料庫，請使用 [發行者屬性 - \<發行者>] 對話方塊的 [發行集資料庫] 頁面。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [Create a Publication](publish/create-a-publication.md)＞。  
  
### <a name="to-enable-a-database-for-replication"></a>若要為複寫啟用資料庫  
  
1.  在 [發行者屬性 - \<發行者>] 對話方塊的 [發行集資料庫] 頁面中，針對您想要複寫的每個資料庫，選取 [異動] 及/或 [合併] 核取方塊。 選取 **[交易式]** 以為快照式複寫啟用資料庫。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  