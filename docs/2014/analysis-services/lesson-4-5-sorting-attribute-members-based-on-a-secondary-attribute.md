---
title: 根據次要屬性排序屬性成員 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 67dacf68-9ab7-4524-8698-844d0f6e6c6d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 067348432bc7a460b4dbf39444852e14c7ef2ce5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "69493898"
---
# <a name="sorting-attribute-members-based-on-a-secondary-attribute"></a>依次要屬性來排序屬性成員
  在第 3 課，您學會如何根據名稱或索引鍵值排序屬性成員。 您也學會如何使用複合成員索引鍵來影響屬性成員和排序次序。 如需詳細資訊，請參閱 [修改 Date 維度](lesson-3-4-modifying-the-date-dimension.md)。 不過，如果屬性的名稱或索引鍵都無法提供想要的排序次序，您可以使用次要屬性來達成所需的排序次序。 藉由定義屬性之間的關聯性，您可以使用次要屬性排序第一個屬性的成員。  
  
 屬性關聯性定義屬性之間的關聯性或相依性。 在以單一關聯式資料表為基礎的維度中，所有屬性通常都是透過索引鍵屬性而彼此相關。 這是因為維度的所有屬性會提供有關成員的資訊，這些成員會由維度的索引鍵屬性連結到各個相關量值群組之事實資料表中的事實。 在以多份資料表為基礎的維度中，屬性通常是依據資料表之間的聯結索引鍵來連結。 如果基礎資料支援屬性關聯性，相關屬性可用來指定排序次序。 例如，您可以建立提供相關屬性排序邏輯的新屬性。  
  
 維度設計師可讓您定義屬性之間的其他關聯性，或變更預設關聯性來增加效能。 當您建立屬性關聯性時，主要條件約束是要確定所參考的屬性對於它相關的屬性中的任何成員只有一個值。 當您在兩個屬性之間定義關聯性時，可以依據成員之間的關聯性是否因為時間而改變來定義固定或彈性關聯性。 例如，員工可能會移至不同的銷售地區，但縣 (市) 卻不會移至不同省份。 如果定義固定關聯性，則每次累加處理維度時不會重新計算屬性彙總。 不過，如果成員之間的關聯性改變，維度必須完全處理。 如需詳細資訊，請參閱 [屬性關聯性](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)、 [定義屬性關聯性](multidimensional-models/attribute-relationships-define.md)、 [設定屬性關聯性屬性](multidimensional-models/attribute-relationships-configure-attribute-properties.md)和 [在使用者定義階層的屬性之間指定屬性關聯性](4-6-specifying-attribute-relationships-in-user-defined-hierarchy.md)。  
  
 在這個主題的工作中，您會根據基礎維度資料表的現有資料行來定義 [日期]**** 維度中的新屬性。 您會使用這個新屬性，按照時間順序而非字母順序來排序日曆月成員。 您也會根據用來排序 [通勤距離]**** 屬性成員的具名計算來定義 [客戶]**** 維度中的新屬性。 在下一個主題的工作中，您會學到如何使用屬性關聯性來增加查詢效能。  
  
## <a name="defining-an-attribute-relationship-and-sort-order-in-the-date-dimension"></a>在日期維度中定義屬性關聯性和排序次序  
  
1.  開啟 [日期]**** 維度的 [維度設計師]，然後在 [屬性] 視窗中檢閱 [月份]**** 屬性 (attribute) 的 [OrderBy]**** 屬性 (property)。  
  
     請注意，[月份]**** 屬性成員是按照索引鍵值來排序。  
  
2.  切換到 [瀏覽器]**** 索引標籤，確認已在 [階層]**** 清單中選取 [日曆日期]****，然後展開使用者定義階層中的層級來檢閱日曆月的排序次序。  
  
     請注意，屬性階層的成員是依據成員索引鍵的 ASCII 值排序，也就是月和年。 在這種情形下，按照屬性名稱或索引鍵排序並不會按時間順序排序日曆月。 若要解決這個問題，您要依據一個新屬性來排序屬性階層的成員，亦即 [MonthNumberOfYear]**** 屬性。 您將根據已存在於 [日期]**** 維度資料表中的資料行來建立這個屬性。  
  
3.  切換到 [日期] 維度的 [維度結構]**** 索引標籤，然後以滑鼠右鍵按一下 [資料來源檢視]**** 窗格中的 [MonthNumberOfYear]****，然後按一下 [從資料行新增屬性]****。  
  
4.  在 [屬性]**** 窗格中，選取 [Month Number Of Year (年中的月份)]****，然後在 [屬性] 視窗中將 [AttributeHierarchyEnabled]**** 屬性設為 [False]****、將 [AttributeHierarchyOptimizedState]**** 屬性設為 [NotOptimized]****，並將 [AttributeHierarchyOrdered]**** 屬性設為 [False]****。  
  
     這些設定會把屬性隱藏起來，讓使用者看不到它們，並改善處理時間。 這個屬性不會用於瀏覽， 它只會用於排列另一個屬性成員的順序。  
  
    > [!NOTE]  
    >  如果依字母順序排序 [屬性] 視窗中的屬性，將可簡化這項工作，因為這三個屬性在排序後將會彼此相鄰。  
  
5.  按一下 **[屬性關聯性]** 索引標籤。  
  
     請注意，[日期]**** 維度中的所有屬性都與 [日期]**** 屬性直接相關，而該屬性是成員索引鍵，它會使維度成員與相關量值群組中的事實產生關聯。 不過，[月份]**** 屬性和 [Month Number Of Year (年中的月份)]**** 屬性之間沒有定義關聯性。  
  
6.  在圖表中，以滑鼠右鍵按一下 [月份]**** 屬性，然後選取 [新增屬性關聯性]****。  
  
7.  在 [建立屬性關聯性]**** 對話方塊中，[來源屬性]**** 是 [月份]****。 將 [相關屬性]**** 設定為 [Month Number Of Year (年中的月份)]****。  
  
8.  在 [關聯性類型]**** 清單中，將關聯性類型設定為 [固定]****。  
  
     [月份]**** 屬性和 [Month Number Of Year (年中的月份)]**** 屬性的成員之間的關聯性不會隨時間而改變。 因此，在累加式處理期間，Analysis Services 不會卸除此關聯性的彙總。 如果真的發生變更，在累加式處理期間將會產生處理錯誤，到時候您就必須執行維度的完整處理。 現在您可以設定 [月份]**** 之成員的排序順序。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. 按一下 [維度結構]**** 索引標籤。  
  
11. 在 [屬性]**** 窗格中選取 [月份]****，然後將 [屬性] 視窗中的 [OrderBy]**** 屬性值變更為 [AttributeKey]****，將 [OrderByAttribute]**** 屬性值變更為 [Month Number Of Year (年中的月份)]****。  
  
12. 在 [建立]**** 功能表上，按一下 [部署 Analysis Services 教學課程]****。  
  
13. 順利完成部署之後，請切換到 [日期] 維度的 [瀏覽器]**** 索引標籤，並按一下 [重新連接]****，然後瀏覽 [日曆日期]**** 和 [會計日期]**** 使用者階層，以確認月份現在是按照時間順序排序。  
  
     請注意，月份現在是按照時間順序排序，如下圖所示。  
  
     ![依時間順序的已修改使用者階層](../../2014/tutorials/media/l4-memberproperties-3.gif "依時間順序的已修改使用者階層")  
  
## <a name="defining-attribute-relationships-and-sort-order-in-the-customer-dimension"></a>在客戶維度中定義屬性關聯性和排序順序  
  
1.  切換至 [客戶] 維度之 [維度設計師] 的 [瀏覽器]**** 索引標籤，然後瀏覽 [通勤距離]**** 屬性階層的成員。  
  
     請注意，這個屬性階層的成員是依據成員索引鍵的 ASCII 值排序。 在這種情形下，按照屬性名稱或索引鍵排序並不會將通勤距離從小排到大。 在這項工作中，您會根據 **CommuteDistanceSort** 具名計算來排序屬性階層的成員，而適當的排序編號將歸因於資料行的每一個相異值。 為了節省時間，這個具名計算已經新增至 **DW 資料來源檢視的** Customer [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 資料表。 您可以切換至這個資料來源檢視，以便檢視此具名計算中使用的 SQL 指令碼。 如需詳細資訊，請參閱[在資料來源檢視中定義具名計算 &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)。  
  
     下圖顯示 [通勤距離]**** 屬性階層的成員，它們是按照成員索引鍵的 ASCII 值來排序。  
  
     ![通勤距離屬性階層](../../2014/tutorials/media/l4-memberproperties-4.gif "通勤距離屬性階層")  
  
2.  切換到 [客戶] 維度之 [維度設計師] 的 [維度結構]**** 索引標籤，並以滑鼠右鍵按一下 [資料來源檢視]**** 窗格中的 [客戶]**** 資料表的 [通勤距離排序]****，然後按一下 [從資料行新增屬性]****。  
  
3.  在 [屬性]**** 窗格中，選取 [通勤距離排序]****，然後在 [屬性] 視窗中將這個屬性的 [AttributeHierarchyEnabled]**** 屬性設為 [False]****、將 [AttributeHierarchyOptimizedState]**** 屬性設為 [NotOptimized]****，並將 [AttributeHierarchyOrdered]**** 屬性設為 [False]****。  
  
     這些設定會把屬性隱藏起來，讓使用者看不到它們，並改善處理時間。 這個屬性不會用於瀏覽， 它只會用於排列另一個屬性成員的順序。  
  
4.  選取 [地理位置]****，然後在 [屬性] 窗格中將它的 [AttributeHierarchyVisible]**** 屬性設為 [False]****、將它的 [AttributeHierarchyOptimizedState]**** 屬性設為 [NotOptimized]****，並且將它的 [AttributeHierarchyOrdered]**** 屬性設為 [False]****。  
  
     這些設定會把屬性隱藏起來，讓使用者看不到它們，並改善處理時間。 這個屬性不會用於瀏覽， 它只會用於排列另一個屬性成員的順序。 因為 [地理位置]**** 具有成員屬性，所以其 [AttributeHierarchyEnabled]**** 屬性必須設定為 [True]****。 因此，若要隱藏該屬性 (attribute)，您可以將 [AttributeHierarchyVisible]**** 屬性 (property) 設定為 [False]****。  
  
5.  按一下 **[屬性關聯性]** 索引標籤。  
  
6.  在屬性清單中，以滑鼠右鍵按一下 [通勤距離]**** 屬性，然後選取 [新增屬性關聯性]****。  
  
7.  在 [建立屬性關聯性]**** 對話方塊中，[來源屬性]**** 是 [通勤距離]****。 將 [相關屬性]**** 設定為 [通勤距離排序]****。  
  
8.  在 [關聯性類型]**** 清單中，將關聯性類型設定為 [固定]****。  
  
     [通勤距離]**** 屬性和 [通勤距離排序]**** 屬性的成員之間的關聯性不會隨時間而改變。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     現在您可以設定 [通勤距離]**** 屬性的排序順序。  
  
10. 按一下 [維度結構]**** 索引標籤。  
  
11. 在 [屬性]**** 窗格中選取 [通勤距離]****，並將 [屬性] 視窗中的 [OrderBy]**** 屬性值變更為 [AttributeKey]****，然後將 [OrderByAttribute]**** 屬性值變更為 [通勤距離排序]****。  
  
12. 在 [建立]**** 功能表上，按一下 [部署 Analysis Services 教學課程]****。  
  
13. 順利完成部署之後，切換到 [客戶] 維度之 [維度設計師] 的 [瀏覽器]**** 索引標籤，並按一下 [重新連接]****，然後瀏覽 [通勤距離]**** 屬性階層。  
  
     請注意，屬性階層成員現在是依據遞增的距離按邏輯順序排序，如下圖所示。  
  
     ![重新排序的通勤距離屬性階層](../../2014/tutorials/media/l4-memberproperties-5.gif "重新排序的通勤距離屬性階層")  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [在使用者定義階層的屬性之間指定屬性關聯性](4-6-specifying-attribute-relationships-in-user-defined-hierarchy.md)  
  
  
