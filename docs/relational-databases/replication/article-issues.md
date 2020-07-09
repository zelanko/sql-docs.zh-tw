---
title: 發行項問題 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.articleissues.f1
ms.assetid: bde57da2-dd47-412f-9df7-9224968b2448
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 02f4089ba5f8f9536c3481dbb34bdbbbe8f795ba
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727246"
---
# <a name="article-issues"></a>發行項的問題
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **[發行項的問題]** 頁面會列出已經發現的發行項狀況，以及這些狀況之結果所需的任何變更。 下表列出可能的問題與確保複寫和現有的應用程式正常運作所需的動作。  
  
|發行項的問題|詳細資料|必要的動作|  
|-------------------|-------------|---------------------|  
|Uniqueidentifier 資料行將被加入至資料表。|複寫需要允許更新訂閱的合併式發行集或交易式發行集內之所有發行項的資料類型為 **uniqueidentifier** 資料行。|複寫會自動將資料類型為 **uniqueidentifier** 的資料行，加入至產生第一個快照集時沒有該資料行的發行資料表中。 您必須確定參考這些資料表的 INSERT 與 UPDATE 陳述式使用資料行清單。 還要確定磁碟上有足夠的空間供其他資料行使用。|  
|IDENTITY 資料行需要 NOT FOR REPLICATION 選項。|複寫需要所有的 IDENTITY 資料行使用 NOT FOR REPLICATION 選項。 如果發行的 IDENTITY 資料行未使用此選項，則 INSERT 命令可能無法正確複寫。|這適用於在執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 和更舊版本的發行者上所建立發行集。 您必須為所有 IDENTITY 資料行指定 NOT FOR REPLICATION 屬性。|  
|IDENTITY 屬性未傳送到訂閱者。|此發行集不允許在訂閱者端更新。 當 IDENTITY 資料行傳送給訂閱者時，不會傳送 IDENTITY 屬性。 例如，在發行者端定義為 INT IDENTITY 的資料行會在訂閱者端定義為 INT。|這適用於在執行 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 和更舊版本之發行者上建立的發行集。 不需要採取任何動作。|  
|需要檢視所參考的資料表。|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要檢視與索引檢視表所參考的已發行資料表都可以在訂閱者端使用。 如果參考的資料表未在此發行集內發行為發行項，就必須手動在訂閱者端建立這些資料表。|使用 **[上一步]** 按鈕，即可導覽至 **[發行項]** 頁面。 加入任何必要的物件。|  
|需要預存程序所參考的物件。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要已發行預存程序所參考的所有物件，例如資料表與使用者自訂函數，都可以在訂閱者端使用。 如果參考的物件未在此發行集內發行為發行項，就必須手動在訂閱者端建立這些物件。|使用 **[上一步]** 按鈕，即可導覽至 **[發行項]** 頁面。 加入任何必要的物件。|  
  
## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [建立發行集](../../relational-databases/replication/publish/create-a-publication.md)  
  
  
