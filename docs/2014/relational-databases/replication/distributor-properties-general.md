---
title: 散發者屬性、一般 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.configdistwizard.distproperties.general.f1
helpviewer_keywords:
- Distributor Properties dialog box
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1a92d36dab69d6602fa9397473ee77133affe80f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136133"
---
# <a name="distributor-properties-general"></a>散發者屬性，一般
  **[散發者屬性]** 對話方塊的 **[一般]** 頁面可讓您加入和刪除散發資料庫，以及設定散發資料庫屬性。  
  
 散發資料庫會儲存所有複寫類型的中繼資料和記錄資料，以及異動複寫的交易。 在許多情況下，單一散發資料庫即已足夠。 但是如果多個發行者使用單一散發者，請考慮為每個發行者建立散發資料庫。 這樣可以確保流經每個散發資料庫的資料都不同。  
  
## <a name="options"></a>選項。  
 **資料庫**  
 **[資料庫]** 屬性方格會顯示散發者上之散發資料庫的名稱與保留屬性。 **[交易保留]** 是為異動複寫儲存交易的時間長度 (交易保留也稱為散發保留)。 **[記錄保留]** 是為所有的複寫類型儲存記錄中繼資料的時間長度。 如需散發保留的詳細資訊，請參閱[訂閱逾期與停用](subscription-expiration-and-deactivation.md)。  
  
 按一下 **[資料庫]** 屬性方格中的屬性按鈕 ( **...** )，即可啟動 **[散發資料庫屬性]** 對話方塊。  
  
 **新增**  
 按一下即可建立新的散發資料庫。  
  
 **刪除**  
 在 **[資料庫]** 屬性方格中選取現有的散發資料庫，然後按一下 **[刪除]** 以刪除資料庫。 如果只有一個這種資料庫，就無法刪除此散發資料庫；每個散發者至少必須有一個散發資料庫。 若要刪除所有的散發資料庫，您必須停用電腦上的散發。 如需詳細資訊，請參閱[停用發行和散發](disable-publishing-and-distribution.md)。  
  
 **設定檔預設值**  
 按一下即可存取 **[代理程式設定檔]** 對話方塊中的複寫代理程式設定檔。 如需有關設定檔的詳細資訊，請參閱＜ [Replication Agent Profiles](agents/replication-agent-profiles.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [[設定散發]](configure-distribution.md)   
 [檢視及修改散發者和發行者屬性](view-and-modify-distributor-and-publisher-properties.md)  
  
  