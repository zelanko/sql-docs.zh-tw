---
title: "概觀：匯出資料 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
caps.latest.revision: 12
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 40f4ec6f9d1e30676dfba32288384a6f0b6fcc6e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="overview-exporting-data-master-data-services"></a>概觀：匯出資料 (Master Data Services)
  本文將介紹訂閱檢視格式類型，以及如何判斷何時因模型物件變更而需要編輯檢視。  
  
 您可以建立訂閱檢視，將 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料匯出至訂閱系統 (例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)])。 您可以使用訂閱系統來檢視 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中的資料。  如需如何建立訂閱檢視的資訊，請參閱 [建立訂閱檢視以匯出資料 &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
 如需檢視的詳細資訊，請參閱 [檢視](../relational-databases/views/views.md)。  
  
## <a name="subscription-view-formats"></a>訂閱檢視格式  
 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]當您在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中建立檢視時，可以從  提供的一組標準檢視格式中選擇。 您可以使用這些格式來建立顯示下列項目的檢視表：  
  
-   所有分葉成員及其屬性。  
  
-   所有合併成員及其屬性。  
  
-   所有集合及其屬性。  
  
-   明確加入至集合的成員。  
  
-   在衍生階層中的父子式或層級格式成員。  
  
-   在所有明確階層中，實體的父子式或層級格式成員。  
  
## <a name="subscription-views-can-become-out-of-date"></a>訂閱檢視可能過期  
 在建立實體或階層的訂閱檢視之後，檢視中未自動反映相關聯的模型物件變更。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 您可能需要在 中重新產生訂閱檢視，以反映模型物件變更。 當模型物件變更時， **[匯出]** 頁面上的 **[已變更]** 欄會更新為 **True** 。 **True** 表示您應該編輯並儲存訂閱檢視，藉以重新產生訂閱檢視。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立主要資料的訂閱檢視。|[建立訂閱檢視以匯出資料 &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|刪除現有的訂閱檢視。|[刪除訂閱檢視 &#40;Master Data Services&#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [訂閱檢視格式 &#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [檢視](../relational-databases/views/views.md)  
  
  

