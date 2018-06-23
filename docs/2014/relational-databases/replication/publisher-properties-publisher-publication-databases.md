---
title: 發行者屬性 - 發行者，發行集資料庫 | Microsoft Docs
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
- sql12.rep.configdistwizard.pubproperties.pubdb.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: 574ea2e7-4e7b-4733-ab52-429ca93c7b0a
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 894d55e77baa9fc0d86e83fe442f2639ea45c559
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36147127"
---
# <a name="publisher-properties---publisher-publication-databases"></a>發行者屬性 - 發行者，發行集資料庫
  **[發行者屬性]** 對話方塊的 **[發行集資料庫]** 頁面，可讓 **系統管理員 (sysadmin)** 固定伺服器角色中的使用者啟用資料庫供複寫。 啟用資料庫不會發行此資料庫；不過，它允許該資料庫之 **db_owner** 固定資料庫角色中的任何使用者在資料庫上建立一個或多個發行集。  
  
## <a name="options"></a>選項。  
 **異動**  
 選取此核取方塊即可讓 **db_owner** 固定資料庫角色中的使用者，在資料庫中建立快照式發行集或交易式發行集。  
  
 **合併式**  
 選取此核取方塊即可讓 **db_owner** 固定資料庫角色中的使用者，在資料庫中建立合併式發行集。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](view-and-modify-distributor-and-publisher-properties.md)   
 [屬性參考 &#40;複寫&#41;](properties-reference-replication.md)  
  
  