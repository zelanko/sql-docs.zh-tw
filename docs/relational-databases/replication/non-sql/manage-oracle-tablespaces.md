---
title: 管理 Oracle 資料表空間 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d3c63ddd5932e5f97fd0dd2b7b05ab657651af9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="manage-oracle-tablespaces"></a>管理 Oracle 資料表空間
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  資料表空間是資料庫的儲存單位，大致相當於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的檔案群組。 資料表空間允許在個別群組中儲存和管理資料庫物件。 如需詳細資訊，請參閱 Oracle 文件集。  
  
 將資料表設定為 Oracle 發行集的一部分，您可以在儲存複寫記錄資訊時選擇性地指定使用現有的 Oracle 資料表空間。 如果未指定，則複寫物件的資料表空間為與複寫管理使用者結構描述相關的預設資料表空間，該複寫管理使用者結構描述在設定「發行者」時設定。  
  
 **為發行項記錄資料表指定資料表空間**：  
  
-   在 **[發行項屬性]** 對話方塊中指定資料表空間。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
-   使用 [sp_changearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)。 若要使用 **sp_changearticle**，請指定下列項目：  
  
    -   **@publisher** 參數的 Oracle 發行者名稱。  
  
    -   **@publication** 參數的 Oracle 發行集名稱。  
  
    -   **@article** 參數的發行項名稱。  
  
    -   參數 **@property**中的檔案群組。  
  
    -   參數 **@value**中的檔案群組。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  
