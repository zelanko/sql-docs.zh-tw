---
title: "HOST_NAME 值 | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.hostnamevalue.f1"
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# HOST_NAME 值
  具有參數化篩選的合併式發行集，會使用 SUSER_SNAME() 函數及/或 HOST_NAME() 函數來篩選資料。 函數是在新增發行集精靈或 **[發行集屬性]** 對話方塊中指定。  
  
 依預設，HOST_NAME() 函數會傳回連接到發行者的電腦名稱。 使用參數化篩選時，通常會在精靈的這個頁面上提供一個值，來覆寫此值。 HOST_NAME() 函數就會傳回您指定的值，而非電腦的名稱。 如需詳細資訊，請參閱 「 覆寫 host_name （） 值 」 一節 [參數化資料列篩選](../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
> [!NOTE]  
>  如果您覆寫 HOST_NAME()，則所有對 HOST_NAME() 函數的呼叫均會傳回您指定的值。 請確定其他應用程式不會相依於由 HOST_NAME() 傳回電腦名稱。  
  
## 選項  
 **訂閱屬性**  
 輸入的值中的每個訂閱者 **HOST_NAME 值** 資料行，或接受預設值，這是訂閱者電腦的名稱。  
  
## 另請參閱  
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME & #40。TRANSACT-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  