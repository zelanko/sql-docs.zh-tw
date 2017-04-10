---
title: "驗證所有訂閱 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.validate.allsubscriptions.f1"
helpviewer_keywords: 
  - "驗證所有訂閱對話方塊"
ms.assetid: 32e31469-36e4-42d9-a57a-12388bfd229d
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 驗證所有訂閱
  使用 **[驗證所有訂閱]** 對話方塊來指定下次執行每個訂閱的合併代理程式時，應驗證合併發行集的所有訂閱。 驗證的結果會在複寫監視器中顯示。 如需詳細資訊，請參閱 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  
  
 它也可讓驗證單一訂閱中的訂閱上按一下滑鼠右鍵 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 按一下 **驗證訂閱**。  
  
## 選項  
 **只確認資料列計數**  
 選取以驗證訂閱者端之資料表的資料列數目是否與發行者端之資料表的資料列數目相同。 此方法不會驗證資料列的內容是否相符。 資料列計數驗證提供一種輕量型驗證方法，可讓您發現資料中的問題。  
  
 **確認資料列計數並比較總和檢查碼，來確認資料列資料**  
 除了統計「發行者」與「訂閱者」上的資料列數量之外，也會使用二進位總和檢查碼演算法計算所有資料的總和檢查碼。 如果資料列計數失敗，就不會執行總和檢查碼。 這個選項對於 [!INCLUDE[ssEW](../../includes/ssew-md.md)]無效。  
  
## 另請參閱  
 [驗證複寫的資料](../../relational-databases/replication/validate-replicated-data.md)  
  
  