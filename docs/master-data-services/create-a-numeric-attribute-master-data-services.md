---
description: 建立數值屬性 (Master Data Services)
title: 建立數值屬性
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating number attributes
- creating number attributes [Master Data Services]
ms.assetid: c0dbb6d8-ba78-485a-a40d-6d5cb7e75d0a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9b22726ec69e1e06ab51ae0f367f3038089e8b25
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461846"
---
# <a name="create-a-numeric-attribute-master-data-services"></a>建立數值屬性 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  當您想要讓使用者輸入數字作為屬性值時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中建立數值屬性。  
  
> [!NOTE]  
>  數值屬性有限制。 如需詳細資訊，請參閱 [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
-   建立屬性的實體必須存在。 如需詳細資訊，請參閱 [建立實體 &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)。  
  
## <a name="attribute-information"></a>屬性資訊  
 針對每個建立的屬性，會將含有七個資料行的資料列加入方格中。 下表描述該資料行。  
  
|資料行|描述|  
|------------|-----------------|  
|狀態|屬性狀態。<br /><br /> 當您按一下 [儲存] 時，會顯示 ![更新狀態](../master-data-services/media/mds-statusicon-updating.png "更新狀態的圖示") 影像的圖示，表示屬性正在更新。<br /><br /> 如果建立或編輯屬性時發生錯誤，則會顯示 ![錯誤狀態](../master-data-services/media/mds-statusicon-error.png "錯誤狀態圖示") 影像的圖示。<br /><br /> 否則，狀態會是 [確定]，而且會顯示 [ ![確定] 狀態](../master-data-services/media/mds-statusicon-ok.png "[確定] 狀態的圖示") 影像的圖示。|  
|名稱|屬性名稱。|  
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
  
### <a name="to-create-a-numeric-attribute"></a>若要建立數值屬性  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [ **管理模型** ] 頁面上，從方格中選取模型，然後按一下 [ **實體**]。  
  
3.  在 [管理實體] **** 頁面上，選取您要為其建立屬性之實體的資料列。  
  
4.  按一下 **[屬性]**。  
  
5.  在 [管理屬性] **** 頁面上，執行下列其中一項動作，然後按一下 [加入] ****。  
  
    -   如果是分葉成員的屬性，請選取 [成員類型] **** 清單方塊的 [分葉] **** 。  
  
    -   如果是合併成員的屬性，請選取 [成員類型] **** 清單方塊的 [合併] **** 。  
  
    -   如果是集合的屬性，請選取 [成員類型] **** 清單方塊的 [集合] **** 。  
  
6.  在 **[名稱]** 方塊中，輸入屬性的名稱。 如需不應該當做屬性名稱使用的單字清單，請參閱 [&#40;Master Data Services&#41;的保留字 ](../master-data-services/reserved-words-master-data-services.md)。  
  
7.  (選擇性) 輸入顯示名稱，然後在 [描述] **** 方塊中輸入屬性的描述。  
  
8.  在 **[顯示像素寬度]** 方塊中，輸入要在 **[總管]** 方格中顯示的屬性資料行寬度。  
  
9. 從 [屬性類型]**** 清單中，選取 [自由格式]****。  
  
10. 從 [資料類型]**** 清單中，選取 [數字]****。  
  
11. 在 [小數]**** 方塊中，輸入可以在小數點後面輸入的位數。  
  
12. 從 [輸入遮罩]**** 清單方塊中，選取負數的格式。  
  
13. (選擇性) 選取 **[啟用變更追蹤]** 以追蹤屬性群組的變更。 如需詳細資訊，請參閱[將屬性加入至變更追蹤群組 &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。  
  
14. 按一下 [檔案] 。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [變更屬性名稱和資料類型 &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [建立以網域為基礎的屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [建立檔案屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
