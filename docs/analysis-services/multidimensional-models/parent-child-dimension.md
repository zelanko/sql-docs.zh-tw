---
title: 父子式維度 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f9990103da1de5107ceaf3432f4da2a9a4486c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208580"
---
# <a name="parent-child-dimension"></a>父子式維度
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  父子式階層是位於包含父屬性之標準維度中的階層。 父屬性描述維度主資料表內的「自我參考關聯性」  或「自我聯結」  。 父子式階層是由單一父屬性所建構的。 因為階層中的層級是從與父屬性相關之成員間的父子式關聯性衍生而來，所以只會將一個層級指派給父子式階層。 父子式階層中之成員的位置是由父屬性 (attribute) 的 **KeyColumns** 和 **RootMemberIf** 屬性 (property) 所決定，而層級中之成員的位置是由父屬性 (attribute) 的 **OrderBy** 屬性 (property) 所決定。 如需屬性 (attribute) 之屬性 (property) 的詳細資訊，請參閱 [屬性和屬性階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)。  
  
 因為在父子式階層內有層級之間的父子式關聯性，所以除了有彙總自子成員的資料以外，部分非分葉成員還可能會有衍生自基礎資料來源的資料。  
  
## <a name="dimension-schema"></a>維度結構描述  
 父子式階層的維度結構描述，相依於維度主資料表上所顯示的自我參考關聯性。 例如，下圖說明 **範例資料庫中的** DimOrganization [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 維度主資料表。  
  
 ![DimOrganization 資料表中的自我參考聯結](../../analysis-services/multidimensional-models/media/dimorganization.gif "DimOrganization 資料表中的自我參考聯結")  
  
 在這份維度資料表中， **ParentOrganizationKey** 資料行與 **OrganizationKey** 主索引鍵資料行具有外部索引鍵關聯性。 換句話說，此資料表中的每一個記錄均可透過父子式關聯性與資料表中的另一個記錄相關。 這種自我聯結通常用來呈現組織實體資料 (例如，部門內之員工的管理結構)。  
  
## <a name="hierarchies-and-levels"></a>階層和層級  
 沒有父子式關聯性的維度是藉由群組和排序屬性來建構階層。 這些維度會從屬性名稱衍生其階層的層級名稱。  
  
 然而，父子式維度會檢查維度主資料表所含的資料，然後評估資料表中之記錄間的父子式關聯性，以建構父子式階層。 如需父子式階層的詳細資訊，請參閱 [使用者階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)。  
  
 父子式階層並不會從用來建立階層的屬性中，衍生出父子式階層中的層級名稱。 相反地，這些維度建立層級名稱會自動使用命名範本的字串運算式，您可以在指定的父屬性，控制如何將屬性產生屬性階層的層級。 如需如何設定父屬性之命名範本的詳細資訊，請參閱 [屬性和屬性階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)。  
  
## <a name="data-members"></a>資料成員  
 通常，維度中的分葉成員會包含直接衍生自基礎資料來源的資料，而非分葉成員則會包含衍生自子成員上所執行之彙總的資料。  
  
 但是父子式階層除了彙總自子成員的資料以外，也可能會有部分非分葉成員的資料是衍生自基礎資料來源。 針對父子式階層中的這些非分葉成員，可以建立特殊、由系統產生的子成員，其中包含基礎事實資料表的資料。 這些特殊子成員稱為 *資料成員*，包含與非分葉成員直接相關聯而且與非分葉成員的下階導出之摘要值無關的值。 如需資料成員的詳細資訊，請參閱 [父子式階層中的屬性](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)。  
  
## <a name="see-also"></a>另請參閱  
 [父子式階層中的屬性](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)   
 [資料庫維度屬性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)  
  
  
