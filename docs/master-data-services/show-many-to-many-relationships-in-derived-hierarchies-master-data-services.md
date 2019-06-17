---
title: 在衍生階層 (Master Data Services) 中顯示多對多關聯性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 8b2a9c43-40e0-48f7-a6a9-325beb9f27da
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4215753da5ef7f9bce51cd7bea8c87551e369da6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488070"
---
# <a name="show-many-to-many-relationships-in-derived-hierarchies-master-data-services"></a>在衍生階層 (Master Data Services) 中顯示多對多關聯性

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  衍生階層 (DH) 顯示一對多關聯性，現今也可以顯示多對多關聯性。  
  
## <a name="many-to-many-m2m-relationships"></a>多對多 (M2M) 關聯性  
 兩個實體之間的多對多 (M2M) 關聯性可能會透過使用第三個實體 (該實體提供兩者間的對應)，進而模型化︰  
  
 ![mds_hierarchies_manytomany](../master-data-services/media/mds-hierarchies-manytomany.png "mds_hierarchies_manytomany")  
  
 在上述範例中， **Employee** 和 **TrainingClass** 實體具有 M2M 關係，其為對應實體 **ClassRegistration**所提供。 員工可能會在多個課程中註冊為學生，而且每個課程可能包含多位學生。  
  
 先前，衍生階層無法將 M2M 關聯性模型化。 自 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]起，您現今可以建立衍生階層，其可顯示像是依據課程的學生，或反轉關聯性並顯示依據學生分組的課程。  
  
 首先，請移至 [衍生階層] 管理頁面，並建立新的衍生階層︰  
  
 ![mds_hierarchies_add_derived_hierarchy](../master-data-services/media/mds-hierarchies-add-derived-hierarchy.png "mds_hierarchies_add_derived_hierarchy")  
  
 接著，從底部開始，將層級加入新衍生階層中。 在此範例中，我們想要顯示依課程分組的學生 (員工)。 因此， **Employee** 實體是階層的分葉層級，且為第一個加入的項目︰  
  
 ![mds_hierarchies_edit_derived_hierarchy_one](../master-data-services/media/mds-hierarchies-edit-derived-hierarchy-one.PNG "mds_hierarchies_edit_derived_hierarchy_one")  
  
 在上面的螢幕擷取畫面中，注意 **Employee** 實體作為中間唯一的層級顯示在 [目前層級]  之下。 右邊的衍生階層 [預覽]  只會顯示 **Employee** 實體的所有成員清單。 左邊的 [可用層級]  區段會顯示哪些層級可能會新增至目前最上層的上方 (**Employee**)。 大多數為 **Employee** 實體上以網域為基礎的屬性 (DBA)，包括 **Department** DBA。  
  
 自 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 開始，有新類型的層級可將 M2M 關聯性模型化，例如：**Class (mapped via ClassRegistration.Student)** 。 層級名稱會比其他項目具備更多詳細資訊，以反映所需的額外資訊，進而明確地描述對應的關聯性。 將此層級拖放至 [目前層級]  區段中的 **Employee** 層級︰  
  
 ![mds_hierarchies_edit_derived_hierarchy_two](../master-data-services/media/mds-hierarchies-edit-derived-hierarchy-two.PNG "mds_hierarchies_edit_derived_hierarchy_two")  
  
 現在預覽會顯示依其所註冊的培訓課程所分組的員工。 由於這是 M2M 關聯性，每個子成員皆可以有多個父系。 在上述範例中，員工 **6 {Hillman, Reinout N}** 在兩堂課程中註冊為學生，分別為 **1 {Master Data Services 101}** 和 **4 {Career-Limiting Moves}** 。  
  
 此對應關聯性也可反轉顯示，將課程依據學生分組︰  
  
 ![mds_hierarchies_available_entities_and_hierarchies](../master-data-services/media/mds-hierarchies-available-entities-and-hierarchies.PNG "mds_hierarchies_available_entities_and_hierarchies")  
  
 同樣地，我們看到子系可出現在多個父系下︰培訓課程 **1 {Master Data Services 101}** 同時出現在 **6 {Hillman, Reinout N}** 和 **40 {Ford, Jeffrey L}** 之下。  
  
 對應實體 **ClassRegistration** 的成員不會在衍生階層內的任何位置出現。 其僅用來定義階層中父系和子系成員之間的關聯性。  
  
 您可以透過修改對應的實體成員來編輯 M2M 關聯性，方法是執行下列其中一項。 M2M 關聯性在 [衍生階層總管]  頁面中為唯讀。  
  
-   修改 [實體總管]  頁面中的對應實體成員，方法是使用適用於 Excel 的 Master Data Services 增益集，或使用資料暫存。  
  
-   拖放 [衍生階層探索]  頁面中父代之間的子節點。  
  
     這個方法會在允許的情況下修改現有的成員，並視需要新增新成員。 不會刪除現有的成員。  
  
     以 ClassRegistration 對應實體為例，將學生移到未使用的節點時，相對應對應實體成員的課程屬性值會變更為 null，且不會刪除該成員。 相反地，將學生從未使用的節點移動至部分課程時，若有現有的對應成員對應到課程為 null 的學生，該成員會進行修改，將課程從 null 變更為新父系。 若找不到任何這類成員，則會新增一個。  
  
     此程序可避免刪除成員，以避免不必要地刪除其他使用者資料；例如，若對應實體除了兩個定義父子式關聯性的屬性以外，還包含其他屬性。 使用者必須明確地直接在對應實體上進行刪除。  
  
 新的 M2M 層級可以出現在衍生階層內的任何位置，前提為該位置允許以網域為基礎的屬性 (DBA)。 M2M 層級可以在最上方，如同上述範例。 其可以在 DBA 層級上方及/或下方，包括遞迴層級。 其可以在明確階層 (已過時) 端點層級之下。 多個 M2M 關聯性可以在相同的衍生階層中鏈結在一起。  
  
 M2M 層級可能會隱藏起來，就像其他衍生階層層級一樣。  
   
### <a name="M2MSample"></a> 範例模型中的 M2M 關聯性  
如需 M2M 關聯性的示範，請檢視 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]隨附之 Customer 範例模型中的 Region Climate 衍生階層。   
  
如下圖所示，建立此關聯性模型的層級名稱是 ![mds_Number1](../master-data-services/media/mds-number1.png)**Climate (透過 RegionClimate.Region 進行對應)** 。 ![mds_Number2](../master-data-services/media/mds-number2.png)**預覽** 會顯示依相關聯氣候類型分組的地區。 這是 M2M 關聯性，原因是有與多個氣候 (父系) 相關聯的地區 (子成員)。 例如， ![mds_Number3](../master-data-services/media/mds-number3.png)**APCR {Asia Pacific}** 是與 ![mds_Number4](../master-data-services/media/mds-number4.png)**A {Tropical}** 和 ![mds_Number5](../master-data-services/media/mds-number5.png)**B {Dry}** 相關聯。  
  
![mds_M2MRelationship_Example_CustomerModel](../master-data-services/media/mds-m2mrelationship-example-customermodel.png)  
  
如需部署 Customer 範例模型的指示，以及 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]隨附的其他範例模型，請參閱 [部署範例模型和資料](~/master-data-services/sql-server-samples-model-deployment-packages-mds.md)。   
  
## <a name="one-many-relationship"></a>一對多關聯性  
 DH 的成員可能是許多子成員的父系，但通常不能有一個以上的父代 (對於例外狀況，請參閱 [成員安全性](#bkmk_member_security))。 例如，假設有兩個實體：Employee 和 Department，其中每一位員工皆屬於單一部門。 此關聯性是透過加入 Employee 實體進行模型化，其為參考 Department 實體的以網域為基礎的屬性 (DBA)︰  
  
 ![mds_hierarchies_onetomany](../master-data-services/media/mds-hierarchies-onetomany.png "mds_hierarchies_onetomany")  
  
 這是一對多關聯性，因為每一位員工皆屬於一個部門，但每個部門皆可以有多個員工。 可能會建立衍生階層，其會顯示依部門分組的員工︰  
  
 ![mds_hierarchies_dh_screenshot](../master-data-services/media/mds-hierarchies-dh-screenshot.png "mds_hierarchies_dh_screenshot")  
  
##  <a name="bkmk_member_security"></a> 成員安全性  
 可讓成員重複的階層 (允許成員有一個以上的父系) 不能用來指派成員安全性權限。 例如：  
  
-   遞迴衍生階層 (RDH)，其未錨點 null 遞迴 (遞迴層級的每個成員皆會出現在 ROOT 與其遞迴父系之下)。  
  
-   遞迴衍生階層，其具有在遞迴層級之上的層級 (遞迴層級的每個成員皆會出現在非遞迴父系與其遞迴父系之下)。  
  
-   衍生階層，其具有 M2M 層級 (子系可能對應至多個父系)。  
  
## <a name="collections"></a>集合  
 集合和明確階層已被取代。 轉換預存程序 (udpConvertCollectionAndConsolidatedMembersToLeaf) 會將集合成員轉換為分葉成員，並建立多對多衍生階層，以擷取集合成員資格的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [衍生階層 &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
