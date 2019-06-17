---
title: 建立日期屬性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- creating date attributes [Master Data Services]
- attributes [Master Data Services], creating date attributes
ms.assetid: 22a8f1a3-b4f2-4cfa-8495-7daad5ce9d12
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1284a15e16465962e2ce2c286bfb2897bb297622
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483354"
---
# <a name="create-a-date-attribute-master-data-services"></a>建立日期屬性 (Master Data Services)
  當您想要讓使用者輸入日期做為屬性值時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中建立日期屬性。  
  
> [!NOTE]  
>  該屬性稱為 DateTime，但不支援時間值。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   您必須有要建立屬性的實體。 如需詳細資訊，請參閱[建立實體 &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-entity-master-data-services.md)。  
  
### <a name="to-create-a-date-attribute"></a>若要建立日期屬性  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]** 。  
  
2.  在 **[模型檢視]** 頁面上，從功能表列指向 **[管理]** ，然後按一下 **[實體]** 。  
  
3.  在 **[實體維護]** 頁面上，選取 **[模型]** 清單中的模型。  
  
4.  針對要建立屬性的實體選取資料列。  
  
5.  按一下 **[編輯選取的實體]** 。  
  
6.  在 **[編輯實體]** 頁面上：  
  
    -   如果是分葉成員的屬性，則按一下 **[分葉成員屬性]** 窗格中的 **[加入分葉屬性]** 。  
  
    -   如果是合併成員的屬性，則按一下 **[合併成員屬性]** 窗格中的 **[加入合併屬性]** 。  
  
    -   如果是集合的屬性，則按一下 **[集合屬性]** 窗格中的 **[加入集合屬性]** 。  
  
7.  選取 **[加入屬性]** 頁面上的 **[自由格式]** 選項。  
  
8.  在 **[名稱]** 方塊中，輸入屬性的名稱。 如需不應該當做屬性名稱使用的字詞清單，請參閱[保留字 &#40;Master Data Services&#41;](../../2014/master-data-services/reserved-words-master-data-services.md)。  
  
9. 在 **[顯示像素寬度]** 方塊中，輸入要在 **[總管]** 方格中顯示的屬性資料行寬度。  
  
10. 從 **[資料類型]** 清單中，選取 **[日期時間]** 。  
  
11. 從 **[輸入遮罩]** 清單中選取日期格式。  
  
12. (選擇性) 選取 **[啟用變更追蹤]** 以追蹤屬性群組的變更。 如需詳細資訊，請參閱[將屬性加入至變更追蹤群組 &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。  
  
13. 按一下 **[儲存屬性]** 。  
  
14. 按一下 **[實體維護]** 頁面上的 **[儲存實體]** 。  
  
## <a name="to-display-the-time-portion-of-a-datetime-value"></a>若要顯示日期時間值的時間部分  
 若要讓使用者介面顯示日期時間值的時間部分，您必須選擇適用於屬性的輸入遮罩。 日期時間屬性的內建遮罩都無法執行這項處理，但是您可以加入可讓您顯示時間的新遮罩。 若要這樣做，請在儲存內建遮罩之 MDS 資料庫的 mdm.tblList 資料表中加入資料列。 此資料列應該有下列值：  
  
|||  
|-|-|  
|ListCode|lstInputMask|  
|ListName|[輸入遮罩]|  
|Seq|19|  
|List Option|dd/MM/yyyy hh:mm:ss tt|  
|Option ID|19|  
|IsVisible|1|  
|Group_ID|3|  
  
 當您在 mdm.tblList 資料表中輸入包含上述值的資料列之後，[輸入遮罩] 清單方塊中將會提供 "dd/MM/yyyy hh:mm:ss tt" 遮罩。 然後，您可以選取該遮罩，在 MDS Explorer 中實體的日期時間屬性資料行中顯示日期和時間。  
  
 輸入遮罩是自訂的 .NET DateTime 格式字串。 如需詳細資訊，請參閱 [自訂日期和時間格式字串](https://msdn.microsoft.com/library/8kb3ddd4\(v=vs.110\).aspx)  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)   
 [變更屬性名稱&#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)   
 [建立網域屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [建立檔案屬性 &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
