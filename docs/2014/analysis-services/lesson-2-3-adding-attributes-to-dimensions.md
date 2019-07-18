---
title: 將屬性加入至維度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 80551dad-97ac-40d0-90af-b810780321ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a30424ce322ed356870465422c4f82fb8d7d88d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079025"
---
# <a name="adding-attributes-to-dimensions"></a>將屬性加入至維度
  既然您已經定義維度，就可以使用代表維度中每個資料元素的屬性擴展它們。 屬性通常是以資料來源檢視中的欄位為基礎。 將屬性加入至維度時，您可以將欄位從任何資料表加入至資料來源檢視中。  
  
 在此工作中，您將使用維度設計師，將屬性加入至 [客戶] 和 [產品] 維度。 根據 [客戶] 和 [地理位置] 資料表中的欄位，[客戶] 維度將包含屬性。  
  
## <a name="adding-attributes-to-the-customer-dimension"></a>將屬性加入至 [客戶] 維度  
  
#### <a name="to-add-attributes"></a>加入屬性  
  
1.  針對 [客戶] 維度開啟維度設計師。 若要這樣做，請在方案總管的 [維度]  節點中，按兩下 [客戶]  維度。  
  
2.  在 [屬性]  窗格中，注意由 Cube 精靈所建立的 [客戶索引鍵] 和 [地理位置索引鍵] 屬性。  
  
3.  在 [維度結構]  索引標籤的工具列上，確定用來檢視 [資料來源檢視]  窗格中資料表的 [顯示比例] 圖示設為 100%。  
  
4.  將下列資料行，從 [資料來源檢視]  窗格中的 [客戶]  資料表拖曳至 [屬性]  窗格：  
  
    -   **BirthDate**  
  
    -   **MaritalStatus**  
  
    -   **Gender**  
  
    -   **EmailAddress**  
  
    -   **YearlyIncome**  
  
    -   **TotalChildren**  
  
    -   **NumberChildrenAtHome**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **HouseOwnerFlag**  
  
    -   **NumberCarsOwned**  
  
    -   **Phone**  
  
    -   **DateFirstPurchase**  
  
    -   **CommuteDistance**  
  
5.  將下列資料行，從 [資料來源檢視]  窗格中的 [地理位置]  資料表拖曳至 [屬性]  窗格：  
  
    -   **City**  
  
    -   **StateProvinceName**  
  
    -   **EnglishCountryRegionName**  
  
    -   **PostalCode**  
  
6.  按一下 [檔案] 功能表上的 [全部儲存]  。  
  
## <a name="adding-attributes-to-the-product-dimension"></a>將屬性加入至 [產品] 維度  
  
#### <a name="to-add-attributes"></a>加入屬性  
  
1.  針對 [產品] 維度開啟維度設計師。 按兩下方案總管中的 [產品]  維度。  
  
2.  在 [屬性]  窗格中，注意由 Cube 精靈所建立的 [產品金鑰] 屬性。  
  
3.  在 [維度結構]  索引標籤的工具列上，確定用來檢視 [資料來源檢視]  窗格中資料表的 [顯示比例] 圖示設為 100%。  
  
4.  將下列資料行，從 [資料來源檢視]  窗格中的 [產品]  資料表拖曳至 [屬性]  窗格：  
  
    -   **StandardCost**  
  
    -   **Color**  
  
    -   **SafetyStockLevel**  
  
    -   **ReorderPoint**  
  
    -   **ListPrice**  
  
    -   **大小**  
  
    -   **SizeRange**  
  
    -   **Weight**  
  
    -   **DaysToManufacture**  
  
    -   **ProductLine**  
  
    -   **DealerPrice**  
  
    -   **類別**  
  
    -   **樣式**  
  
    -   **ModelName**  
  
    -   **StartDate**  
  
    -   **EndDate**  
  
    -   **狀態**  
  
5.  按一下 [檔案] 功能表上的 [全部儲存]  。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [檢閱 Cube 和維度屬性](lesson-2-4-reviewing-cube-and-dimension-properties.md)  
  
## <a name="see-also"></a>另請參閱  
 [維度屬性 (Attribute) 屬性 (Property) 參考](multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
