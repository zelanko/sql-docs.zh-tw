---
title: "佇列讀取器代理程式安全性 | Microsoft Docs"
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
- sql13.rep.security.QRA.f1
helpviewer_keywords:
- Queue Reader Agent Security dialog box
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 58afa56e66377ea4ac00bd9296128bbe7483719c
ms.lasthandoff: 04/11/2017

---
# <a name="queue-reader-agent-security"></a>佇列讀取器代理程式安全性
  **[佇列讀取器代理程式安全性]** 對話方塊，可以讓您指定執行佇列讀取器代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶，以及進行本機連接到散發者。 代理程式會使用 **[發行者屬性]** 對話方塊 (可從 **[散發者屬性]** 對話方塊取得) 指定的帳戶，來連接到發行者；另外，代理程式會使用與散發代理程式用於訂閱的相同內容，來連接到訂閱者。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 帳戶必須有效，並且要指定正確的密碼。 等到代理程式執行時，才會驗證帳戶與密碼。  
  
## <a name="options"></a>選項  
 **處理帳戶**  
 輸入在散發者端執行佇列讀取器代理程式的 Windows 帳戶。 您指定的 Windows 帳戶，至少必須是散發資料庫中之 **db_owner** 固定資料庫角色的成員。  
  
 **[密碼]** 與 **[確認密碼]**  
 輸入 Windows 帳戶的密碼。  
  
## <a name="see-also"></a>另請參閱  
 [管理複寫的登入與密碼](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
