---
title: 取代的 Master Data Services 功能 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: lrtoyou1223
ms.author: lle
manager: erikre
ms.openlocfilehash: d08fd9bbb91a3783cf176f150fc966d1b44a2fc4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65485287"
---
# <a name="deprecated-master-data-services-features"></a>取代的 Master Data Services 功能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主題描述 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中仍然可用但已被取代的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。 這些功能將在未來的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本中移除。 已被取代的功能不應在新應用程式中使用。  
  
## <a name="explicit-hierarchies-collections-and-related-components"></a>明確階層、集合和相關元件  
 已取代明確階層、集合和相關元件。 先前模型化為合併成員類型 (明確階層父系) 和集合成員類型的成員，日後則會模式化為衍生階層中的分葉成員。 下列新功能讓衍生階層取代明確階層。  
  
-   遞迴衍生階層現在可用來指派成員安全性權限。  
  
     明確階層類似於使用遞迴層級下單一非遞迴層級的遞迴衍生階層。 遞迴衍生階層可能因為包含位在遞迴層級上及 (或) 下的層級，而變得複雜。  
  
-   在總管中，衍生階層頁面現在會顯示每個階層層級未指派 (未使用) 的成員。 未使用的節點會依階層層級分組。 可以藉由拖放或剪下及貼上的方式，在未使用節點和根節點間移動成員。  
  
     在 [系統管理] 中，未使用的節點會顯示在 [預覽]  窗格中。 在 [安全性] 中，未使用的節點會顯示在 [階層成員權限]  窗格中。 可以將權限指派給位在 [根]  節點或 [未使用]  節點下的成員。 也可以將權限指派給 [根]  、[未使用]  和 [未使用]  虛擬成員。  
  
-   預存程序 mdm.udpConvertCollectionAndConsolidatedMembersToLeaf 將明確階層轉換為遞迴衍生階層，並將合併成員和集合成員轉換為分葉成員。  
  
     明確階層、合併和集合成員類型仍受支援，因此不一定要執行預存程序。 不過如果您使用這些已取代的項目，建議您執行預存程序。  
  
 如需明確階層、集合和合併成員的相關資訊，請參閱下列主題。  
  
-   [明確階層 &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [集合 &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [成員 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
## <a name="attribute-entity-transaction-log-type"></a>屬性實體交易記錄類型  
已淘汰 [屬性] 實體交易記錄類型，請移轉至 [成員] 實體交易記錄類型。 如需實體交易記錄類型的相關資訊，請參閱下列主題：
* [變更實體交易記錄類型 (Master Data Services)](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)
* [成員修訂歷程記錄](../master-data-services/member-revision-history-master-data-services.md)
  
## <a name="external-resources"></a>外部資源  
 msdn.com 上的部落格文章：[已淘汰：Explicit Hierarchies and Collections](https://go.microsoft.com/fwlink/p/?LinkId=615373) (明確階層和集合)。  
  
## <a name="see-also"></a>另請參閱  
 [已停止的 Master Data Services 功能](../master-data-services/discontinued-master-data-services-features.md)  
  
  
