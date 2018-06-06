---
title: 回復成員修訂歷程記錄 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c59d60c0c9f6eb24b124134330f1da29e4176195
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="rollback-member-revision-history-master-data-services"></a>回復成員修訂歷程記錄 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  每次變更成員時會記錄成員修訂歷程記錄。 您可以將成員修訂歷程記錄回復至舊版。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   您必須具有更新至少一個選取的成員之屬性的權限。 當您復原修訂歷程記錄時，可更新的所有屬性值將會都回復為先前的版本值。  
  
-   修訂歷程記錄只有在實體的交易記錄類型為成員時可用。  
  
 **若要回復成員修訂歷程記錄**  
  
1.  在 [主資料管理員] 中，按一下 [總管]。  
  
2.  選擇要復原的實體和成員。  
  
3.  按一下 [檢視歷程記錄]。  
  
4.  選擇要回復的修訂，然後按一下 [回復]。  
  
## <a name="see-also"></a>另請參閱  
 [成員修訂歷程記錄 &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [變更實體交易記錄類型 &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  
