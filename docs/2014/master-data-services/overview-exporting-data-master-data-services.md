---
title: 匯出資料 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f92a74caa74c5cf15e917cd6c15aef9506a60180
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482844"
---
# <a name="exporting-data-master-data-services"></a>匯出資料 (Master Data Services)
  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 您可以建立訂閱檢視，將  資料匯出至訂閱系統。 
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 然後，任何訂閱系統可以檢視  資料庫中的已發行資料。 如需檢視的更多資訊，請參閱[檢視](../relational-databases/views/views.md)。  
  
## <a name="subscription-view-formats"></a>訂閱檢視格式  
 
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]當您在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中建立檢視時，可以從  提供的一組標準檢視格式中選擇。 您可以使用這些格式來建立顯示下列項目的檢視表：  
  
-   所有分葉成員及其屬性。  
  
-   所有合併成員及其屬性。  
  
-   所有集合及其屬性。  
  
-   明確加入至集合的成員。  
  
-   在衍生階層中的父子式或層級格式成員。  
  
-   在所有明確階層中，實體的父子式或層級格式成員。  
  
## <a name="subscription-views-can-become-out-of-date"></a>訂閱檢視可能過期  
 在建立實體或階層的訂閱檢視之後，檢視中未自動反映相關聯的模型物件變更。 
  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 您可能需要在 中重新產生訂閱檢視，以反映模型物件變更。 當模型物件變更時， **[匯出]** 頁面上的 **[已變更]** 欄會更新為 **True** 。 **True**表示您應該編輯訂閱視圖並加以儲存，以重新產生視圖。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立主要資料的訂閱檢視。|[建立訂閱視圖 &#40;Master Data Services&#41;](create-a-subscription-view-to-export-data-master-data-services.md)|  
|刪除現有的訂閱檢視。|[刪除訂閱視圖 &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [訂用帳戶視圖格式 &#40;Master Data Services&#41;](../../2014/master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [檢視](../relational-databases/views/views.md)  
  
  
