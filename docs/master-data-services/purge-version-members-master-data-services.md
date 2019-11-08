---
title: 清除版本成員
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: adecce2d-46bb-49ff-8be9-0b31b8dd3cb6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 94543ada58c5af829da6a7650e21f5f4e2deb9bb
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729015"
---
# <a name="purge-version-members-master-data-services"></a>清除版本成員 [Master Data Services]

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，刪除成員只會停用或虛刪除該名成員。 資料仍然位於資料庫中。 本主題說明如何清除 (永久刪除) 模型版本中所有已虛刪除的成員。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序。  
  
-   您必須具有存取 [版本管理] 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
## <a name="to-purge-soft-deleted-members"></a>清除虛刪除的成員  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[版本管理]** 。  
  
2.  在 [管理版本] 頁面上，選取要清除之版本的模型。 模型版本清單隨即顯示。  
  
3.  選取要清除之版本的資料列。  
  
4.  按一下 [清除成員]。  
  
5.  在確認提示中按一下 [確定]。  
  
## <a name="additional-methods-to-purge-members"></a>清除成員的其他方法  
 清除版本成員會永久刪除與選取的版本相關的所有實體中的虛刪除成員。 更精細的替代方法是使用實體式暫存，僅永久刪除實體的特定成員。 此外，具有 Explorer 功能權限的實體系統管理員可能會在實體總管頁面中清除實體版本。  
  
 如需詳細資訊，請參閱[分葉成員暫存資料表 &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
  
