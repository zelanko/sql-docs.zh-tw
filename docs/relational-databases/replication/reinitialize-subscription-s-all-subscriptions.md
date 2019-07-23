---
title: 重新初始化訂閱 - 所有訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.reinit.all.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: e1122018-9f74-43e3-8489-7eae33ff23d9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 014f8f62d29c149474e68c70efcc4c3c2a80355c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021240"
---
# <a name="reinitialize-subscriptions---all-subscriptions"></a>重新初始化訂閱 - 所有訂閱
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **[重新初始化訂閱]** 對話方塊可以讓您標示發行集的所有訂閱，以進行重新初始化。 重新初始化會牽涉到將快照集套用到每個訂閱者；對於交易式發行集的訂閱，這是由散發代理程式執行；而對於合併式發行集的訂閱，則是由合併代理程式執行。  
  
## <a name="options"></a>選項。  
 **使用目前的快照集**  
 選取即可在散發代理程式或合併代理程式下次針對訂閱執行時，將目前的快照集套用到每個訂閱者。 如果沒有任何有效的快照集可以使用，則不可以選取此選項。  
  
 **使用新的快照集**  
 選取即可使用新的快照集重新初始化所有的訂閱。 唯有在快照集代理程式產生快照集之後，才可以將該快照集套用至每個訂閱者。 如果快照集代理程式已設定為依排程執行，則要等在下一個排程的快照集代理程式執行之後，才會將訂閱重新初始化。  
  
 選取 **[立即產生新的快照集]** ，即可立即啟動快照集代理程式。  
  
 **重新初始化之前，先上傳尚未同步處理的變更**  
 僅限合併式複寫。 選取即可在使用快照集覆寫訂閱者端的資料之前，從訂閱資料庫上傳任何暫止的變更。  
  
 如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。  
  
 **標示為重新初始化**  
 按一下即可標示要重新初始化的每項訂閱。 有效的快照集可以使用之後，下次針對訂閱執行散發代理程式或合併代理程式時，快照集就會在訂閱者端套用。  
  
## <a name="see-also"></a>另請參閱  
 [重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)  
  
  
