---
title: Web 伺服器資訊 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5f5c2385b4c58447db008544124ae9048566958
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63199949"
---
# <a name="web-server-information"></a>Web 伺服器資訊
  使用合併式複寫的 Web 同步處理選項時，需要有 Web 伺服器資訊。 如需設定 Web 同步處理的資訊，請參閱[設定 Web 同步處理](configure-web-synchronization.md)。  
  
## <a name="options"></a>選項。  
 **Web 伺服器位址**  
 如果您在 [發行集屬性]  對話方塊的 [FTP 快照集和網際網路]  頁面中，指定了 Web 伺服器位址，該位址就會在此文字方塊中顯示為預設值。 接受預設值，或輸入同步處理此訂閱的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 伺服器之完整 Web 伺服器位址。  
  
 **每一個訂閱者如何連接到 Web 伺服器？**  
 指定用於連接到 Web 伺服器的驗證類型。 針對 IIS 伺服器連接，建議使用基本驗證搭配安全通訊端層 (SSL)。 如果您選取基本驗證，請輸入從訂閱者連接到 IIS 伺服器時所使用的登入名稱和密碼。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [檢視及修改提取訂閱屬性](view-and-modify-pull-subscription-properties.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [合併式複寫的 Web 同步處理](web-synchronization-for-merge-replication.md)  
  
  
