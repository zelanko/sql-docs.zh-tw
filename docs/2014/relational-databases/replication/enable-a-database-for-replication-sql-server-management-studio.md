---
title: 為複寫啟用資料庫 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server replication]
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 307d52e24187e35c1c30f609facd13bfad569216
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010744"
---
# <a name="enable-a-database-for-replication-sql-server-management-studio"></a>為複寫啟用資料庫 (SQL Server Management Studio)
  **sysadmin** 固定伺服器角色成員使用「新增發行集精靈」建立發行集時，會為複寫隱含啟用資料庫。 **sysadmin** 固定伺服器角色成員同樣可以為複寫明確啟用資料庫，以便 **db_owner** 固定資料庫角色成員可以在該資料庫中建立一個或多個發行集。 若要明確啟用資料庫，請使用 [**發行者屬性- \<Publisher> ** ] 對話方塊的 [發行集**資料庫**] 頁面。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [Create a Publication](publish/create-a-publication.md)＞。  
  
### <a name="to-enable-a-database-for-replication"></a>若要為複寫啟用資料庫  
  
1.  在 [**發行者屬性- \<Publisher> ** ] 對話方塊的 [發行集**資料庫**] 頁面上，針對您要複寫的每個資料庫選取 [**交易**式和/或**合併**] 核取方塊。 選取 **[交易式]** 以為快照式複寫啟用資料庫。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
