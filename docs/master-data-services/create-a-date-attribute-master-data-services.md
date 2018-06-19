---
title: 建立日期屬性 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- creating date attributes [Master Data Services]
- attributes [Master Data Services], creating date attributes
ms.assetid: 22a8f1a3-b4f2-4cfa-8495-7daad5ce9d12
caps.latest.revision: 13
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ce3d934327706eaf7733c5fec22b8e46311aed5a
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35400410"
---
# <a name="create-a-date-attribute-master-data-services"></a>建立日期屬性 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  當您想要讓使用者輸入日期做為屬性值時，可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中建立日期屬性。  
  
> [!NOTE]  
>  該屬性稱為 DateTime，但不支援時間值。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
-   您必須有要建立屬性的實體。 如需詳細資訊，請參閱[建立實體 &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)。  
  
### <a name="to-create-a-date-attribute"></a>若要建立日期屬性  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [管理模型]  頁面上，從方格中選取模型，然後按一下 [實體] 。  
  
3.  在 [管理實體]  頁面上，選取您要為其建立屬性之實體的資料列。  
  
4.  按一下 **[屬性]**。  
  
5.  在 [管理屬性]  頁面上，執行下列其中一項動作，然後按一下 [加入] 。  
  
    -   如果是分葉成員的屬性，請選取 [成員類型]  清單方塊的 [分葉]  。  
  
    -   如果是合併成員的屬性，請選取 [成員類型]  清單方塊的 [合併]  。  
  
    -   如果是集合的屬性，請選取 [成員類型]  清單方塊的 [集合]  。  
  
6.  在 **[名稱]** 方塊中，輸入屬性的名稱。 如需不應該當做屬性名稱使用的字詞清單，請參閱[保留字 &#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md)。  
  
7.  (選擇性) 輸入顯示名稱，然後在 [描述]  方塊中輸入屬性的描述。  
  
8.  在 **[顯示像素寬度]** 方塊中，輸入要在 **[總管]** 方格中顯示的屬性資料行寬度。  
  
9. 從 [屬性類型] 清單中，選取 [自由格式]。  
  
10. 從 **[資料類型]** 清單中，選取 **[日期時間]**。  
  
11. 從 **[輸入遮罩]** 清單中選取日期格式。  
  
12. (選擇性) 選取 **[啟用變更追蹤]** 以追蹤屬性群組的變更。 如需詳細資訊，請參閱[將屬性加入至變更追蹤群組 &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)。  
  
13. 按一下 **[儲存]**。  
  
## <a name="to-display-the-time-portion-of-a-datetime-value"></a>若要顯示日期時間值的時間部分  
 若要讓使用者介面顯示日期時間值的時間部分，您必須選擇適用於屬性的輸入遮罩。 日期時間屬性的內建遮罩都無法執行這項處理，但是您可以加入可讓您顯示時間的新遮罩。 若要這樣做，請在儲存內建遮罩之 MDS 資料庫的 mdm.tblList 資料表中加入資料列。 此資料列應該有下列值：  
  
|||  
|-|-|  
|ListCode|lstInputMask|  
|ListName|[輸入遮罩]|  
|Seq|19|  
|List Option|dd/MM/yyyy hh:mm:ss tt|  
|Option ID|19|  
|IsVisible|@shouldalert|  
|Group_ID|3|  
  
 當您在 mdm.tblList 資料表中輸入包含上述值的資料列之後，[輸入遮罩] 清單方塊中將會提供 "dd/MM/yyyy hh:mm:ss tt" 遮罩。 然後，您可以選取該遮罩，在 MDS Explorer 中實體的日期時間屬性資料行中顯示日期和時間。  
  
 輸入遮罩是自訂的 .NET DateTime 格式字串。 如需詳細資訊，請參閱 [自訂日期和時間格式字串](https://msdn.microsoft.com/en-us/library/8kb3ddd4\(v=vs.110\).aspx)  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [變更屬性名稱和資料類型 &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [建立網域屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [建立檔案屬性 &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
