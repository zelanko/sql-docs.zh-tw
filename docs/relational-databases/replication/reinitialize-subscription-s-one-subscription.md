---
title: "重新初始化訂閱 - 一個訂閱 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.reinit.single.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: 9b0cf0be-d1f1-4163-a0ca-d6f095aa707e
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8fbb60295103fad2edccc62b19c791407148b91
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="reinitialize-subscriptions---one-subscription"></a>重新初始化訂閱 - 一個訂閱
  **[重新初始化訂閱]** 對話方塊可讓您將訂閱標示為重新初始化。 重新初始化包含將快照集套用至訂閱者；針對交易式發行集的訂閱，是由散發代理程式執行，而針對合併式發行集的訂閱，則是由合併代理程式執行。  
  
## <a name="options"></a>選項  
 **使用目前的快照集**  
 選取即可將目前的快照集套用至散發代理程式或合併代理程式下一次將執行的訂閱者。 如果沒有任何有效的快照集可以使用，則不可以選取此選項。  
  
 **使用新的快照集**  
 選取即可使用新的快照集重新初始化訂閱。 唯有在快照集代理程式產生快照集之後，該快照集才能套用至訂閱者。 如果將快照集代理程式設定為依據排程執行，則只有在下一個排程的快照集代理程式執行之後，才會重新初始化訂閱。  
  
 選取 **[立即產生新的快照集]** ，即可立即啟動快照集代理程式。  
  
 **重新初始化之前，先上傳尚未同步處理的變更**  
 僅限合併式複寫。 選取即可在使用快照集覆寫訂閱者端的資料之前，從訂閱資料庫上傳任何暫止變更。  
  
 如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
 **標示為重新初始化**  
 按一下即可將訂閱標示為重新初始化。 有效的快照集可以使用之後，下次針對訂閱執行散發代理程式或合併代理程式時，快照集就會在訂閱者端套用。  
  
## <a name="see-also"></a>另請參閱  
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  
