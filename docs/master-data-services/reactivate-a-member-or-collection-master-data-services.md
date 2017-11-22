---
title: "重新啟用成員或集合 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collections [Master Data Services], reactivating
- consolidated members [Master Data Services], reactivating
- reactivating members [Master Data Services]
- members [Master Data Services], reactivating
- reactivating collections [Master Data Services]
- leaf members [Master Data Services], reactivating
ms.assetid: bb4884c0-3658-4763-92d1-636804278b1c
caps.latest.revision: "11"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e19f066de7f7acd43a49ad6cc525af0eb91e413
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="reactivate-a-member-or-collection-master-data-services"></a>重新啟用成員或集合 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以重新啟用以下成員：  
  
-   已透過暫存處理序停用。  
  
-   已在 MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]中予以刪除。  
  
-   已在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中予以刪除。  
  
 當您重新啟用成員時，即會還原成員在階層和集合中的屬性及其成員資格。  
  
 您也可以重新啟用集合。 當您這麼做時，會還原集合的屬性以及屬於該集合的成員。  
  
 重新啟用集合或成員時，會還原先前所有的交易。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 中，您必須具有 [版本管理] 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md) (管理員 (Master Data Services))。  
  
### <a name="to-reactivate-a-member-or-collection"></a>若要重新啟用成員或集合  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 首頁上，按一下 [版本管理]。  
  
2.  在功能表列上，按一下 [交易]。  
  
3.  在 [交易] 頁面上，選取 [模型] 清單中的模型。  
  
4.  從 **[版本]** 清單中選取版本。  
  
5.  在 [交易] 窗格中，按一下您要重新啟用之成員或集合的資料列。 此資料列應該在 [先前的值] 資料行中顯示 [Active]，並在 [新值] 資料行中顯示 [De-Activated]。  
  
6.  按一下 [反轉交易]。  
  
7.  在確認對話方塊中按一下 **[確定]**。 即會加入新交易，在 [新值] 資料行中顯示 [Active]。  
  
## <a name="see-also"></a>另請參閱  
 [刪除成員或集合 &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)   
 [成員 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [集合 &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  
