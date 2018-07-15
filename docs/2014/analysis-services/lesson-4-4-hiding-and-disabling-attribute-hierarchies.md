---
title: 隱藏及停用屬性階層 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 095039c2-7104-414c-a9a6-327b03ce79df
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d980e87255d24d754e19d8358b423ba38440d05d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271954"
---
# <a name="hiding-and-disabling-attribute-hierarchies"></a>隱藏及停用屬性階層
  根據預設，系統會在維度中建立每個屬性的屬性階層，而且每個階層都可用來建立事實資料的維度。 這個階層是由「全部」層級和詳細資料層級 (含階層的所有成員) 所組成。 如同您已學到的，您可以將屬性組織成使用者自訂階層，在 Cube 中提供導覽路徑。 在某些情況下，您可以停用或隱藏某些屬性及其階層。 例如，某些屬性如保險號碼或身分證號碼、薪水、出生日期和登入資訊等，使用者不能利用這些屬性來建立 Cube 資訊的維度。 相反地，這項資訊通常只是做為特定屬性成員的詳細資料來檢視。 您可以隱藏這些屬性階層，讓屬性只顯示成特定屬性的成員屬性。 您也可以讓其他屬性的成員 (例如客戶名稱或郵遞區號) 只透過使用者階層而非透過獨立屬性階層來檢視。 這麼做的原因是為了顯示屬性階層中的全部相異成員。 最後，為了增進處理效能，您應該將使用者不再用來瀏覽的屬性階層停用。  
  
 **AttributeHierarchyEnabled** 屬性的值決定是否建立屬性階層。 如果這個屬性設為 **False**，則不建立屬性階層，且屬性不得做為使用者階層中的一個層級；屬性階層只得以成員屬性的身分存在。 不過，已停用的屬性階層仍然可以用來排序另一個屬性的成員。 如果 **AttributeHierarchyEnabled** 屬性的值設為 **True**，則 **AttributeHierarchyVisible** 屬性的值將決定是否不論屬性階層在使用者自訂階層中的用法為何皆會顯示。  
  
 啟用屬性階層之後，您可以指定下列另外 3 個屬性的值：  
  
-   **IsAggregatable**  
  
     依預設，會對所有屬性階層定義 (全部) 層級。 若要為啟用的屬性階層停用 (全部) 層級，請將這個屬性的值設為 **False**。  
  
    > [!NOTE]  
    >  如果某個屬性的 **IsAggregatable** 屬性設為 false，其就只能當做使用者定義階層的根使用，而且必須指定預設的成員 (否則， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 引擎將會為您選擇一個成員)。  
  
-   **AttributeHierarchyOrdered**  
  
     依預設， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在處理期間會排序已啟用屬性階層的成員，然後按 **OrderBy** 屬性的值來儲存成員，例如按名稱或索引鍵。 如果您不在乎排序，可將這個屬性的值設為 **False**，來增加處理效能。  
  
-   **AttributeHierarchyOptimizedState**  
  
     依預設， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在處理期間會為每一個已啟用的屬性階層建立一個索引，來改進查詢效能。 如果您不打算使用屬性階層來瀏覽，可將這個屬性的值設為 **NotOptimized**，來增加處理效能。 不過，如果您使用隱藏的階層做為維度的索引鍵屬性，則建立屬性成員的索引仍然可以改進效能。  
  
 如果屬性階層已停用，則這些屬性不適用。  
  
 在這個主題的工作中，您會在 [員工] 維度中停用不用於瀏覽的保險號碼和其他屬性。 然後您會在 [客戶] 維度中隱藏客戶名稱和郵遞區號屬性階層。 這些階層中大量的屬性成員會使得瀏覽這些階層的速度變得很慢 (與使用者階層無關)。  
  
## <a name="setting-attribute-hierarchy-properties-in-the-employee-dimension"></a>在 [員工] 維度中設定屬性階層的屬性  
  
1.  切換到適用於 [員工] 維度的維度設計師，然後按一下 [瀏覽器] 索引標籤。  
  
2.  確認下列屬性階層有出現在 [階層] 清單中：  
  
    -   **底薪**  
  
    -   **Birth Date**  
  
    -   **登入識別碼**  
  
    -   **管理員 SSN**  
  
    -   **SSN**  
  
3.  切換至 [維度結構] 索引標籤，然後在 [屬性] 窗格中選擇下列屬性。 您可以在按住 CTRL 鍵的同時，按一下每個量值，藉以選取多個量值：  
  
    -   **底薪**  
  
    -   **Birth Date**  
  
    -   **登入識別碼**  
  
    -   **管理員 SSN**  
  
    -   **SSN**  
  
4.  在 [屬性] 視窗中，針對已選取的屬性，將 **AttributeHierarchyEnabled** 屬性的值設為 **False**。  
  
     請注意，在 [屬性] 窗格中，每個屬性的圖示已變更為指示該屬性未啟用。  
  
     下圖顯示針對已選取的屬性，將 **AttributeHierarchyEnabled** 屬性設為 False。  
  
     ![AttributeHierarchyEnabled 屬性設為 False](../../2014/tutorials/media/l4-hierarchyenabled-1.gif "AttributeHierarchyEnabled 屬性設為 False")  
  
5.  在 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
6.  順利完成處理之後，切換到 [瀏覽器] 索引標籤、按一下 [重新連接]，然後試著瀏覽已修改的屬性階層。  
  
     請注意，已修改屬性的成員不會顯示在 [階層] 清單中的屬性階層，供您瀏覽。 如果您嘗試加入其中一個已停用的屬性階層做為使用者階層中的一個層級，您會收到錯誤訊息，通知您必須啟用屬性階層才能參與使用者自訂階層。  
  
## <a name="setting-attribute-hierarchy-properties-in-the-customer-dimension"></a>在客戶維度中設定屬性階層的屬性  
  
1.  切換到適用於 [客戶] 維度的維度設計師，然後按一下 [瀏覽器] 索引標籤。  
  
2.  確認下列屬性階層有出現在 [階層] 清單中：  
  
    -   **全名**  
  
    -   **Postal Code**  
  
3.  切換到 [維度結構] 索引標籤，然後使用 CTRL 鍵同時選取多個屬性，來選取 [屬性] 窗格中的下列屬性：  
  
    -   **全名**  
  
    -   **Postal Code**  
  
4.  在 [屬性] 視窗中，針對已選取的屬性，將 **AttributeHierarchyVisible** 屬性的值設為 **False** 。  
  
     因為這些屬性階層的成員將用於建立事實資料的維度，所以將這些屬性階層的成員排序和最佳化，可改進效能。 因此，不得變更這些屬性的屬性。  
  
     下圖顯示 **AttributeHierarchyVisible** 屬性設為 False。  
  
     ![AttributeHierarchyVisible 屬性設為 False](../../2014/tutorials/media/l4-hierarchyvisible-1.gif "AttributeHierarchyVisible 屬性設為 False")  
  
5.  從 [屬性] 窗格，將 [郵遞區號] 屬性拖曳到 [客戶地理位置] 使用者階層中 (位於 [階層和層級] 窗格的 [縣 (市)] 層級下)。  
  
     請注意，隱藏的屬性仍然成為使用者階層中的一個層級。  
  
6.  在 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
7.  順利完成部署之後，針對 [客戶] 維度切換到 [瀏覽器] 索引標籤，然後按一下 [重新連接]。  
  
8.  嘗試從 [階層] 清單中選取任何一個已修改的屬性階層。  
  
     請注意，兩個已修改的屬性階層都不會出現在 [階層] 清單中。  
  
9. 在 [階層] 清單中，選取 [客戶地理位置]，然後在瀏覽器窗格中瀏覽每一個層級。  
  
     請注意，[郵遞區號] 和 [全名] 這兩個隱藏的層級會出現在使用者自訂階層中。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [依次要屬性來排序屬性成員](../analysis-services/lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md)  
  
  
