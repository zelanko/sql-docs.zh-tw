---
title: "MSSQL_ENG002601 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG002601 錯誤"
ms.assetid: 657c3ae6-9e4b-4c60-becc-4caf7435c1dc
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG002601
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2601|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱|不適用|  
|訊息文字|無法在物件中插入重複的索引鍵資料列 '%.* ls' 具有唯一索引' %。\*ls'。|  
  
## 說明  
 這是不論複寫資料庫與否，都有可能發生的一般性錯誤。 在複寫資料庫中，通常是因為主要索引鍵未於拓撲之間適當管理，才會發生這個錯誤。 在散發環境中，務必確認主要索引鍵資料行或其他唯一資料行中，並未於多個節點插入相同的值。 可能的原因包括：  
  
-   同時在多個節點發生資料列的插入與更新動作。 合併式複寫與異動複寫的可更新訂閱，皆提供衝突偵測和解決方案，但最好還是在單一節點插入或更新給定資料列。 點對點交易不提供衝突偵測和解決方案；必須先分割插入與更新。  
  
-   插入訂閱者的資料列應該是唯讀的。 快照集發行集的訂閱者應設定唯讀，交易式發行集的訂閱者亦同；除非已使用可更新訂閱或點對點異動複寫。  
  
-   已使用具有識別欄位的資料表，但並未適當管理資料行。  
  
-   在合併式複寫中，此亦會發生錯誤時，插入系統資料表 **MSmerge_contents**; 引發的錯誤如下︰ 無法在具有唯一索引 'ucl1SycContents'。 物件 'MSmerge_contents' 中插入重複的索引鍵資料列  
  
## 使用者動作  
 必須依照錯誤產生的原因採取動作：  
  
-   同時在多個節點發生資料列的插入與更新動作。  
  
     不論使用哪一種複寫類型，建議您隨時分割插入和更新；因為這樣可以減少衝突偵測與解決方案所需的處理。 點對點異動複寫需要分割插入和更新。 如需詳細資訊，請參閱 [端對端交易式複寫](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
-   插入訂閱者的資料列應該是唯讀的。  
  
     請勿於訂閱者插入或更新資料列，除非您使用合併式複寫、有可更新訂閱的異動複寫或點對點異動複寫。  
  
-   已使用具有識別欄位的資料表，但並未適當管理資料行。  
  
     針對合併式複寫以及有可更新訂閱的異動複寫，應由複寫來自動管理識別欄位。 點對點異動複寫必須手動管理。 如需詳細資訊，請參閱 [複寫識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
-   就會發生錯誤時，插入系統資料表 **MSmerge_contents**。  
  
     此錯誤可能是因為聯結篩選屬性值不正確 **join_unique_key**。 只有在父資料表中的聯結資料行為唯一時，此屬性才應設定為 TRUE。 如果屬性設定為 TRUE，但是資料行不是唯一的，則會引發此錯誤。 如需有關如何設定這個屬性的詳細資訊，請參閱 [定義及修改聯結篩選之間合併發行項](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  