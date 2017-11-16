---
title: "散發者屬性、一般 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.configdistwizard.distproperties.general.f1
helpviewer_keywords: Distributor Properties dialog box
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64544ff33771c0718a7a22694087ffaa67928a80
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="distributor-properties-general"></a>散發者屬性，一般
  **[散發者屬性]** 對話方塊的 **[一般]** 頁面可讓您加入和刪除散發資料庫，以及設定散發資料庫屬性。  
  
 散發資料庫會儲存所有複寫類型的中繼資料和記錄資料，以及異動複寫的交易。 在許多情況下，單一散發資料庫即已足夠。 但是如果多個發行者使用單一散發者，請考慮為每個發行者建立散發資料庫。 這樣可以確保流經每個散發資料庫的資料都不同。  
  
## <a name="options"></a>選項  
 **資料庫**  
 **[資料庫]** 屬性方格會顯示散發者上之散發資料庫的名稱與保留屬性。 **[交易保留]** 是為異動複寫儲存交易的時間長度 (交易保留也稱為散發保留)。 **[記錄保留]** 是為所有的複寫類型儲存記錄中繼資料的時間長度。 如需散發保留的詳細資訊，請參閱[訂閱逾期與停用](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 按一下**[資料庫]**屬性方格中的屬性按鈕 ( **...** )，即可啟動 **[散發資料庫屬性]** 對話方塊。  
  
 **新增**  
 按一下即可建立新的散發資料庫。  
  
 **Delete**  
 在 **[資料庫]** 屬性方格中選取現有的散發資料庫，然後按一下 **[刪除]** 以刪除資料庫。 如果只有一個這種資料庫，就無法刪除此散發資料庫；每個散發者至少必須有一個散發資料庫。 若要刪除所有的散發資料庫，您必須停用電腦上的散發。 如需詳細資訊，請參閱[停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)。  
  
 **設定檔預設值**  
 按一下即可存取 **[代理程式設定檔]** 對話方塊中的複寫代理程式設定檔。 如需有關設定檔的詳細資訊，請參閱＜ [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [設定散發](../../relational-databases/replication/configure-distribution.md)   
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
