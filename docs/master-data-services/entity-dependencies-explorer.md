---
title: 實體相依性總管 | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
keywords:
- Master Data Services
ms.assetid: 9d922118-1412-4a9d-9c02-70d6c48d6c0d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 18c25a5ec9dfb17039baf11e66b3f4e2c7244552
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483965"
---
# <a name="entity-dependencies-explorer"></a>Entity Dependencies (實體相依性) 總管

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 2016 所加入的新總管頁面 ([實體相依性]) 提供替代方式，來視覺化模型內實體成員間的關聯性 (透過其網域屬性 (DBA) 值所指定)，但不需要先定義 [衍生階層]。   
  
它有助於回答「誰正在使用我的實體，且其做法為何？」問題。 此檢視與 [衍生階層] 總管頁面類似，但它包含的範圍更廣。 它會顯示所有 DBA 關聯性，而不只是定義為特定階層一部分的 DBA 關聯性。 不需要階層定義，因為只會從現有 DBA 推斷所顯示的階層結構。  
  
在 [總管] 頁面功能表中，[Entity Dependencies] (實體相依性) 功能表項目會列出模型中至少有一個實體所相依的所有實體 (即至少有一個實體具有參考所列實體的 DBA)。 實體名稱旁邊會顯示相依性 (直接和間接) 數目，並依這個數目排序清單，而且大量參考的實體會在頂端。 下列螢幕擷取畫面取自 [範例資料](https://msdn.microsoft.com/library/master-data-services-sample.aspx)的客戶模型，並顯示有 7 個實體參考 BigArea 實體 (直接或間接)：  
  
![MDS_EntityDependencies_Menu.jpg](../master-data-services/media/mds-entitydependencies-menu-jpg.jpg)  
    
按一下這個功能表項目會開啟 BigArea 實體的新 [Entity Dependencies] (實體相依性) 總管頁面，這個頁面會顯示如何使用實體成員。 它會在樹狀結構的頂端顯示具有 BigArea 成員的階層檢視，而其 7 個耗用實體的成員巢狀如下：  
  
![MDS_EntityDependencies_Tree.jpg](../master-data-services/media/mds-entitydependencies-tree-jpg.jpg)  
    
多個實體可以直接使用某個實體。 在上述範例中，SubRegion 和 RegionClimate 實體都使用 Region 實體，或具有 Region 實體的 DBA 參考。 每個耗用實體的成員都會一起分組在具有下列實體名稱的父節點下方︰   
  
![MDS_EntityDependencies_Entity_Node.jpg](../master-data-services/media/mds-entitydependencies-entity-node-jpg.jpg)  
  
這些容器樹狀節點是以類似格線的圖示顯示在實體名稱左邊，並且會依階層層級深度將文字著色。 上述範例顯示 "CDSR {Canada}" SubRegion 具有 "CDR {Canada}" Region 的 DBA 參考，而後者所參考的 "CDA {Canada}" Area 參考 "NAm {N. America}" BigArea。  
  
此檢視完全可進行編輯，就像在 [階層總管] 頁面中一樣。 將子成員從某個父系剪下/貼上或拖放到另一個父系，即可修改樹狀結構中的父子關聯性。 在樹狀結構右邊的詳細資料面板中，可能可以修改其他成員屬性值。   
  
  
  
  

