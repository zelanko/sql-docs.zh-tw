---
title: MSSQL_ENG002601 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG002601 error
ms.assetid: 657c3ae6-9e4b-4c60-becc-4caf7435c1dc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a3994aa8a442f0ec1522bdf2314e0d6023e94bcf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52760241"
---
# <a name="mssqleng002601"></a>MSSQL_ENG002601
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2601|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱|N/A|  
|訊息文字|無法以唯一索引 '%.\*ls' 在物件 '%.*ls' 中插入重複的索引鍵資料列。|  
  
## <a name="explanation"></a>說明  
 這是不論複寫資料庫與否，都有可能發生的一般性錯誤。 在複寫資料庫中，通常是因為主要索引鍵未於拓撲之間適當管理，才會發生這個錯誤。 在散發環境中，務必確認主要索引鍵資料行或其他唯一資料行中，並未於多個節點插入相同的值。 可能的原因包括：  
  
-   同時在多個節點發生資料列的插入與更新動作。 合併式複寫與異動複寫的可更新訂閱，皆提供衝突偵測和解決方案，但最好還是在單一節點插入或更新給定資料列。 點對點交易不提供衝突偵測和解決方案；必須先分割插入與更新。  
  
-   插入訂閱者的資料列應該是唯讀的。 快照集發行集的訂閱者應設定唯讀，交易式發行集的訂閱者亦同；除非已使用可更新訂閱或點對點異動複寫。  
  
-   已使用具有識別欄位的資料表，但並未適當管理資料行。  
  
-   在合併式複寫中，這項錯誤也可能在插入作業期間系統資料表**MSmerge_contents**; 引發的錯誤如下：無法以唯一索引 'ucl1syccontents'。' 物件 'MSmerge_contents' 中插入重複的索引鍵資料列  
  
## <a name="user-action"></a>使用者動作  
 必須依照錯誤產生的原因採取動作：  
  
-   同時在多個節點發生資料列的插入與更新動作。  
  
     不論使用哪一種複寫類型，建議您隨時分割插入和更新；因為這樣可以減少衝突偵測與解決方案所需的處理。 點對點異動複寫需要分割插入和更新。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)。  
  
-   插入訂閱者的資料列應該是唯讀的。  
  
     請勿於訂閱者插入或更新資料列，除非您使用合併式複寫、有可更新訂閱的異動複寫或點對點異動複寫。  
  
-   已使用具有識別欄位的資料表，但並未適當管理資料行。  
  
     針對合併式複寫以及有可更新訂閱的異動複寫，應由複寫來自動管理識別欄位。 點對點異動複寫必須手動管理。 如需詳細資訊，請參閱[複寫識別資料欄](publish/replicate-identity-columns.md)。  
  
-   在插入系統資料表 **MSmerge_contents**期間會發生此錯誤。  
  
     發生此錯誤是因為聯結篩選屬性 **join_unique_key**的值不正確。 只有在父資料表中的聯結資料行為唯一時，此屬性才應設定為 TRUE。 如果屬性設定為 TRUE，但是資料行不是唯一的，則會引發此錯誤。 如需有關設定此屬性的詳細資訊，請參閱＜ [定義和修改合併發行項之間的聯結篩選](publish/define-and-modify-a-join-filter-between-merge-articles.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
