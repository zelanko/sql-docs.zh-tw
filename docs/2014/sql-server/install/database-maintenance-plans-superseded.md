---
title: 資料庫維護計畫取代 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- suspended database maintenance plans
- database maintenance plans [SQL Server Agent]
- maintenance plans [SQL Server Agent]
ms.assetid: efac127c-6c81-4c7a-a6c4-9aae5d15545d
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f71e0cb8cb94cba893403f31cb2ffb9ee229c4ca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032708"
---
# <a name="database-maintenance-plans-superseded"></a>已取代資料庫維護計畫
    
## <a name="component"></a>元件  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>描述  
 現有的資料庫維護計劃已經升級，而且仍會繼續運作。 但是，您將無法使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來建立新的資料庫維護計劃。 若要在 [物件總管] 中檢視維護計畫，請展開 [管理]，然後再展開 [舊版]。 您可以將現有的資料庫維護計畫移轉至新格式選取**移轉**從任何資料庫維護計劃的內容功能表。 因為新維護計畫功能並非直接取代資料庫維護計畫，所以移轉後，某些功能可能會遺失。 移轉資料庫維護計畫並不會刪除舊計畫，所以您可以測試維護計畫的功能後，再移除舊計畫。  
  
 資料庫維護計畫不再支援下列功能：  
  
-   記錄傳送  
  
-   **嘗試修復所有次要問題**選項**資料庫完整性檢查**工作  
  
## <a name="corrective-action"></a>更正動作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 禁止在資料庫維護計劃中包含記錄傳送。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜記錄傳送＞。  
  
  