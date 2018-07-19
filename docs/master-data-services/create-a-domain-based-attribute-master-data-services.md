---
title: 建立網域屬性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
caps.latest.revision: 12
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: eaf83f1ebf1b435c5721e10a3b760cc4d15fe3c7
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35335952"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>建立網域屬性 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，建立網域屬性，以使用實體成員來擴展屬性值。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   屬性值的來源實體必須存在。 例如，若要根據色彩實體建立網域屬性，您必須先建立色彩實體。 如需詳細資訊，請參閱[建立實體 &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)。  
  
-   建立屬性的實體必須存在。 如需詳細資訊，請參閱[建立實體 &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)。  
  
## <a name="attribute-information"></a>屬性資訊  
 針對每個建立的屬性，會將含有七個資料行的資料列加入方格中。 下表描述該資料行。  
  
|「資料行」|描述|  
|------------|-----------------|  
|[狀態]|屬性狀態。<br /><br /> 當您按一下 [儲存] 時，會顯示![正在更新狀態圖示](../master-data-services/media/mds-statusicon-updating.png "正在更新狀態圖示")影像，表示正在更新屬性。<br /><br /> 如果建立或編輯屬性時發生錯誤，則會顯示![錯誤狀態圖示](../master-data-services/media/mds-statusicon-error.png "錯誤狀態圖示")影像。<br /><br /> 否則，狀態為正常，並顯示![正常狀態圖示](../master-data-services/media/mds-statusicon-ok.png "正常狀態圖示")影像。|  
|[屬性]|屬性名稱。|  
|顯示名稱|屬性的顯示名稱。|  
|描述|屬性描述。|  
|顯示像素寬度|屬性的寬度。|  
|類型和屬性|屬性的類型和資料類型資訊。|  
|啟用變更追蹤|指定屬性是否已啟用變更追蹤，並在括弧中顯示群組編號。|  
  
 當您按一下屬性時，會顯示下列資訊。  
  
-   **建立者**：建立屬性的使用者名稱。  
  
-   **時間**：建立屬性的日期與時間。  
  
-   **更新者**：上次更新屬性的使用者名稱。  
  
-   **時間**：上次更新屬性的日期與時間。  
  
### <a name="to-create-a-domain-based-attribute"></a>若要建立網域屬性  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型] 頁面上，依序按一下模型與 [實體]。  
  
3.  在 [管理實體] 頁面上，選取您要為其建立屬性之實體的資料列。  
  
4.  按一下 **[屬性]**。  
  
5.  在 [管理屬性]  頁面上，執行下列其中一項動作，然後按一下 [加入] 。  
  
    -   如果是分葉成員的屬性，請選取 [成員類型]  清單方塊的 [分葉]  。  
  
    -   如果是合併成員的屬性，請選取 [成員類型]  清單方塊的 [合併]  。  
  
    -   如果是集合的屬性，請選取 [成員類型]  清單方塊的 [集合]  。  
  
6.  在 **[名稱]** 方塊中，輸入屬性的名稱。 如需不應該當做屬性名稱使用的字詞清單，請參閱[保留字 &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md)。  
  
7.  (選擇性) 輸入顯示名稱，然後在 [描述] 方塊中輸入描述。  
  
8.  在 **[顯示像素寬度]** 方塊中，輸入要在 **[總管]** 方格中顯示的屬性資料行寬度。  
  
9. 從 [屬性類型] 清單中，選取 [網域]。  
  
10. 從 [網域實體] 清單中，選擇要用來擴展屬性值的實體。 
  
11. **(選擇性) 適用於分葉成員的網域屬性。** 選取篩選父屬性，以用來限制允許的網域屬性值。  
  
     篩選父屬性必須是相同實體中分葉成員的另一個網域屬性。 衍生的階層必須具有一個層級，且該層級定義兩個屬性之網域實體間的父子式關聯性。  
  
     如需限制允許的值的資訊，請參閱 Master Data Services 部落格上的 [How to filter Domain Based Attribute drop down lists](https://blogs.msdn.microsoft.com/mds/2015/12/03/in-sql-server-2016-master-data-services-how-to-filter-domain-based-attribute-drop-down-lists/)(如何篩選網域屬性下拉式清單)。  
  
12. **選擇性。** 選取 [啟用變更追蹤] 以追蹤屬性群組的變更。 如需詳細資訊，請參閱[將屬性加入至變更追蹤群組 &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。  
  
13. 按一下 **[儲存]**。  
  
## <a name="see-also"></a>另請參閱  
 [網域屬性 &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)   
 [建立衍生階層 &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [變更屬性名稱和資料類型 &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [刪除屬性 &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)  
  
  
