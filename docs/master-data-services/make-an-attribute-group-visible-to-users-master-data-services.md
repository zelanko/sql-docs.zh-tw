---
title: 讓使用者看到屬性群組 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e60b7dd48bc20a43da1bee110eee5662a91d420f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>讓使用者看到屬性群組 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  當您希望使用者在總管 功能區域的方格上方有索引標籤時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中對使用者或群組顯示屬性群組。  
  
 當您建立屬性群組時，它會自動隱藏起來不讓所有使用者看到，除了建立它的使用者以外。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   至少有一個屬性群組必須存在。 如需詳細資訊，請參閱 [建立屬性群組 &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)(管理員 (Master Data Services))。  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>若要讓使用者看到屬性群組  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型]  頁面上，從方格中選取模型，然後按一下 [實體] 。  
  
3.  在 [管理實體] 頁面上，從方格中選取含有您想要編輯屬性群組之實體的資料列。  
  
4.  按一下 [屬性群組]。  
  
5.  在 [管理屬性群組] 頁面上，取決於您想要顯示的群組類型，從 [成員類型] 下拉式清單方塊中選取成員類型，展開 [分葉]、[合併] 或 [集合]。  
  
6.  選取您想要從方格中編輯的屬性群組，然後按一下 [編輯]。  
  
7.  按一下 [可用] 方塊中的使用者或群組，然後按一下 [加入] 箭號。 若要全部加入，請按一下 [全部加入] 箭號。  
  
8.  按一下 **[儲存]**。  
  
## <a name="see-also"></a>另請參閱  
 [屬性群組 &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [建立屬性群組 &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
