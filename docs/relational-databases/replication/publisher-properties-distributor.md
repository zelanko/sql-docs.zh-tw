---
title: "發行者屬性 - 散發者 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.configdistwizard.distpubproperties.f1
helpviewer_keywords: Publisher Properties dialog box
ms.assetid: ab6ada76-0f99-43fe-b524-baac7b1bc483
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: befe4ba107a2e9fd37a106668c9b87fa5c068060
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="publisher-properties---distributor"></a>發行者屬性 - 散發者
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [發行者屬性] 對話方塊可讓您檢視和修改與發行者及其散發者之間的關聯性建立關聯的屬性。  
  
## <a name="options"></a>選項。  
 **代理程式至發行者的連接**  
 指定下列代理程式用來從散發者連接到發行者的內容。  
  
-   允許佇列更新訂閱之交易式發行集的佇列讀取器代理程式。  
  
-   Oracle 發行集的快照集代理程式和記錄讀取器代理程式。  
  
 選取 **[模擬代理程式處理帳戶]** 來使用執行這些代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶連接到發行者，或指定 **[SQL Server 驗證]**，然後輸入 **[登入]** 和 **[密碼]**的值。 建議您選取 **[模擬代理程式處理帳戶]**。 如需代理程式安全性的詳細資訊，請參閱[複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
 執行這些代理程式的 Windows 帳戶會在新增發行集精靈中指定。 可以在下列位置變更這些帳戶：  
  
-   在佇列讀取器代理程式的 **[散發者屬性]** 對話方塊中。  
  
-   在快照集代理程式和記錄讀取器代理程式的 **[發行集屬性]** 對話方塊中。  
  
 **其他**  
 屬性 **[發行者類型]** 和 **[散發資料庫名稱]** 是唯讀的。 可以變更屬性 **[預設快照集資料夾]** 。 如需快照集資料夾的詳細資訊，請參閱[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [屬性參考 &#40;複寫&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
