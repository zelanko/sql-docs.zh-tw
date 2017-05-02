---
title: "Web 伺服器資訊 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9c3db680206fb7c752fe27f968961d751c78aae0
ms.lasthandoff: 04/11/2017

---
# <a name="web-server-information"></a>Web 伺服器資訊
  使用合併式複寫的 Web 同步處理選項時，需要有 Web 伺服器資訊。 如需設定 Web 同步處理的資訊，請參閱[設定 Web 同步處理](../../relational-databases/replication/configure-web-synchronization.md)。  
  
## <a name="options"></a>選項。  
 **Web 伺服器位址**  
 如果您在 [發行集屬性]**** 對話方塊的 [FTP 快照集和網際網路]**** 頁面中，指定了 Web 伺服器位址，該位址就會在此文字方塊中顯示為預設值。 接受預設值，或輸入同步處理此訂閱的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 伺服器之完整 Web 伺服器位址。  
  
 **每一個訂閱者如何連接到 Web 伺服器？**  
 指定用於連接到 Web 伺服器的驗證類型。 針對 IIS 伺服器連接，建議使用基本驗證搭配安全通訊端層 (SSL)。 如果您選取基本驗證，請輸入從訂閱者連接到 IIS 伺服器時所使用的登入名稱和密碼。  
  
## <a name="see-also"></a>另請參閱  
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [非 SQL Server 訂閱者](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
