---
title: 實體
description: 實體是包含在 Master Data Services 模型中的物件。 每個實體都含有會員，也就是您所管理之主要資料的資料列。
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], about entities
- entities [Master Data Services]
ms.assetid: 0af057d5-6b73-472b-99eb-9f5eb61a9b5b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1b3f7a2645af68f6470aa971feef46fa103556a0
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796316"
---
# <a name="entities-master-data-services"></a>實體 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  實體是 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 模型中包含的物件。 每個實體都含有會員，也就是您所管理之主要資料的資料列。  
  
## <a name="how-many-entities-are-appropriate"></a>多少實體才合適？  
 模型可以包含任何您想要管理的實體數量。 每個實體都應該將類似的資料類型群組在一起。 例如，您可能會想要將一個實體用於您所有的公司帳戶，或是將一個實體用於員工的主要清單。  
  
 一般來說，有一個或多個中央實體對您的公司很重要，而且模型中的其他物件也與這些實體有關。 例如，在 Product 模型中，您可以有一個名為 Product 的中央實體，以及與其他 Product 實體相關，名為 Subcategory 和 Category 的實體。 但是，您不需要有中央實體。 依據您的需求，您可能會有數個您認為同樣重要的實體。  
  
## <a name="how-entities-relate-to-other-model-objects"></a>實體如何與其他的模型物件相關聯  
 您可以將實體視為包含主要資料的資料表，其中資料列代表成員，而資料行代表屬性。  
  
 ![以資料表表示的 Master Data Services 實體](../master-data-services/media/mds-conc-entity-table.gif "以資料表表示的 Master Data Services 實體")  
  
 以您要管理的主要資料清單來擴展實體。  
  
 實體可用來建立衍生階層，也就是以多個實體為基礎的層級型階層。 如需詳細資訊，請參閱 [衍生階層 &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)。  
  
 您也可以讓實體包含明確階層 (以單一實體為基礎的不完全結構) 和集合 (成員子集的 One-off 合併)。 如需詳細資訊，請參閱[明確階層 &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md) 和[集合 &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)。  
  
## <a name="using-entities-as-constrained-lists"></a>使用實體做為條件約束清單  
 當使用者要指派屬性給實體中的成員時，您可以讓他們從條件約束的值清單中選擇。 若要這麼做，您可以使用實體來擴展屬性值的清單。 這稱為網域屬性。 如需詳細資訊，請參閱 [網域屬性 &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)。  
  
## <a name="base-entities"></a>基底實體  
 在模型中導覽物件時，基底實體是使用者的起始點。 基底實體可決定當使用者開啟 **[總管]** 功能區域，並按一下功能表列上的 **[總管]** 時，所呈現的畫面配置。 若要指定實體做為基底實體，請導覽至 **[系統管理]** 功能區域。 在 **[模型檢視]** 頁面上，將實體從右邊的樹狀控制，拖曳至左邊樹狀控制中的模型名稱。  
  
## <a name="entity-security"></a>實體安全性  
 您可以授予使用者實體的權限，包括相關的模型物件。 如需詳細資訊，請參閱[實體權限 &#40;Master Data Services&#41;](../master-data-services/entity-permissions-master-data-services.md)。  
  
## <a name="entity-examples"></a>實體範例  
 下列範例顯示具有下列屬性的實體：Name、Code、Subcategory、StandardCost、ListPrice 和 FilePhoto。 這些屬性描述成員。 每個成員都是由單一資料列的屬性值來表示。  
  
 ![自行車產品實體資料表](../master-data-services/media/mds-conc-entity-table-w-data.gif "自行車產品實體資料表")  
  
 在下列範例中，Product 實體是中央實體。 Subcategory 實體是 Product 實體的網域屬性。 Category 實體是 Subcategory 實體的網域屬性。 StandardCost 和 ListPrice 是 Product 實體的自由格式屬性，FilePhoto 則是 Product 實體的檔案屬性。  
  
 ![產品實體樹狀結構](../master-data-services/media/mds-conc-entity-ui.gif "產品實體樹狀結構")  
  
> [!NOTE]  
>  這是以 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 使用者介面 (UI) 為基礎的範例。 階層樹狀結構會顯示實體與網域屬性之間的關聯性。 這是為了顯示關聯性，而不是為了表示重要性層級。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|建立新實體。|[建立實體 &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)|  
|變更現有實體的名稱。|[編輯實體 &#40;Master Data Services&#41;](../master-data-services/edit-an-entity-master-data-services.md)|  
|刪除現有實體。|[刪除實體 &#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)|  
|將權限指派給實體。|[指派模型物件權限 &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [模型 &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
-   [成員 &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
-   [屬性 &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
