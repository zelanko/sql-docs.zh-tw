---
title: "驗證合併訂閱者的資料分割資訊 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "合併式複寫資料驗證 [SQL Server 複寫], 分割區"
  - "參數化篩選 [SQL Server 複寫], 驗證分割區資訊"
  - "驗證資料分割資訊"
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 驗證合併訂閱者的資料分割資訊
  在為合併式發行集定義參數化資料列篩選器時，可以使用參考「訂閱者」資訊的功能，例如「訂閱者」的登入名稱。 依預設，複寫將在每次同步處理和在「訂閱者」端套用快照集之前，根據該功能驗證「訂閱者」資訊。 驗證處理可確保為每個「訂閱者」正確分割資料。 驗證行為由控制 **validate_subscriber_info** 發行集屬性，可以使用變更 [sp_changemergepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 或在 **訂閱選項** 頁面 **發行集屬性** 對話方塊。 如需變更發行集屬性的詳細資訊，請參閱 [檢視和修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
## 資料分割驗證的運作方式  
 當發行集篩選時，例如，使用函數 **suser_sname （)**, ，「 合併代理程式套用初始快照集的資料是有效的每個訂閱者 **suser_sname （)** 運算式。  
  
 如果在「訂閱者」重新連接到「發行者」以進行下一次同步處理時已啟用驗證，「合併代理程式」便會在「訂閱者」端驗證資訊，並確定每個「訂閱者」的資料分割與初始快照集中接收的資料分割相同。 對於每個後續合併或快照集應用程式，「合併代理程式」會驗證每個「訂閱者」的資料分割。  
  
 如果「合併代理程式」偵測到，篩選運算式中使用的函數傳回不同於初始快照集中獲得的值，合併或快照集應用程式便會失敗，且「訂閱者」的訂閱可能需要重新初始化。 如果「訂閱者」的合併設定發生變更，則可能需要重新初始化以防止出現問題，但在「訂閱者」端將資訊 (例如登入名稱) 變更回原始快照集所使用的值或許已足夠。  
  
 在「合併代理程式」驗證分割時，除了根據篩選運算式中所使用之函數傳回的值來驗證分割外，代理程式還會檢查快照集在使其無效的變更 (例如中繼資料清除作業或結構描述變更) 發生前是否已產生。 如果分割的快照集太舊，「合併代理程式」將傳回錯誤，且您必須根據目前的一般快照集為該「訂閱者」重新產生分割的快照集。  
  
## 另請參閱  
 [管理 & #40。複寫 & #41;](../../relational-databases/replication/administration/administration-replication.md)   
 [複寫管理的最佳做法](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-replicated-data.md)  
  
  