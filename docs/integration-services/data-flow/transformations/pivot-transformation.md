---
title: 樞紐轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.pivottrans.f1
helpviewer_keywords:
- Pivot transformation
- normalized data [Integration Services]
- PivotUsage property
- datasets [Integration Services], normalized data
- less normalized data set [Integration Services]
ms.assetid: 55f5db6e-6777-435f-8a06-b68c129f8437
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6f51c7dc5dcde2535e822a8f1d832e3747bdfd35
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919534"
---
# <a name="pivot-transformation"></a>樞紐轉換

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  「樞紐」轉換可藉由樞紐資料行值上的輸入資料，將正規化的資料集轉換為較不正規但更精簡的版本。 例如，列出客戶名稱、產品及購買數量的正規化 **Orders** 資料集，對於購買多個產品的客戶一般都具有多個資料列，且該客戶的每個資料列都顯示不同產品的訂單詳細資料。 藉由樞紐產品資料行上的資料集，「樞紐」轉換可以為每位客戶輸出含單一資料列的資料集。 該單一資料列會列出客戶購買的所有產品，產品名稱顯示為資料行名稱，而數量則顯示為產品資料行中的值。 因為不是每位客戶都會購買所有產品，所以許多資料行可能包含 Null 值。  
  
 當樞紐資料集時，輸入資料行會在樞紐處理中執行不同的角色。 資料行的參與方式如下：  
  
-   資料行未經變更便傳送至輸出。 因為許多輸入資料列只產生一個輸出資料列，所以轉換僅複製資料行的第一個輸入值。  
  
-   資料行用作識別一組記錄的索引鍵或索引鍵的一部分。  
  
-   資料行定義樞紐。 此資料行中的值與已樞紐之資料集中的資料行關聯。  
  
-   資料行包含樞紐建立之資料行中的值。  
  
 這個轉換有一個輸入、一個規則輸出及一個錯誤輸出。  
  
## <a name="sort-and-duplicate-rows"></a>排序和複製資料列  
 若要有效地樞紐資料 (即在輸出資料集中建立盡可能少的記錄)，輸入資料必須根據樞紐資料行進行排序。 如果資料未排序，「樞紐」轉換可能會為集索引鍵 (定義集成員資格的資料行) 中的每個值產生多筆記錄。 例如，如果資料集在 **Name** 資料行上進行樞紐但名稱未排序，則輸出資料集中的每位客戶可能會一個以上的資料列，因為 **Name** 中的值在每次變更時都會進行樞紐。  
  
 輸入資料可能會包含重複資料列，因而造成「樞紐」轉換失敗。 「重複資料列」表示集索引鍵資料行及樞紐資料行中有相同值的資料列。 若要避免失敗，您可以設定轉換，而將錯誤資料列重新導向至錯誤輸出，也可以預先彙總值，以確定沒有重複資料列。  
  
##  <a name="options-in-the-pivot-dialog-box"></a><a name="options"></a> 樞紐對話方塊中的選項  
 您可以在 [樞紐]  對話方塊中設定選項，以設定樞紐作業。 若要開啟 [樞紐]  對話方塊，請將樞紐轉換加入 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中的封裝，然後以滑鼠右鍵按一下元件，再按一下 [編輯]  。  
  
 下列清單描述 [樞紐]  對話方塊中的選項。  
  
 **樞紐索引鍵**  
 指定要用於跨資料表頂端列 (標頭資料列) 之值的資料行。  
  
 **設定索引鍵**  
 指定要用於資料表左側資料行之值的資料行。 輸入日期必須儲存在此資料行上。  
  
 **樞紐值**  
 指定要用於跨資料表值 (非標頭資料列或左側資料行中的值) 的資料行。  
  
 **忽略不相符的樞紐索引鍵值，並在 DataFlow 執行後回報**  
 選取此選項可將樞紐轉換設定為忽略包含 [樞紐索引鍵]  資料行中未辨識之值的資料列，並在執行封裝時，將所有樞紐索引鍵值輸出至記錄訊息。  
  
 您也可以將 **PassThroughUnmatchedPivotKeys** 自訂屬性設定為 [True]  ，以便將轉換設定為輸出值。  
  
 **根據值產生樞紐輸出資料行**  
 在此方塊中輸入樞紐索引鍵值，讓樞紐轉換針對每個值建立輸出資料行。 您可以在執行封裝之前輸入值，或執行下列操作。  
  
1.  選取 [忽略不相符的樞紐索引鍵值，並在 DataFlow 執行後回報]  選項，然後在 [樞紐]  對話方塊中按一下 [確定]  ，以儲存樞紐轉換的變更。  
  
2.  執行封裝。  
  
3.  當封裝成功時，按一下 [進度]  索引標籤，然後從包含樞紐索引鍵值的樞紐轉換中尋找資訊記錄訊息。  
  
4.  以滑鼠右鍵按一下訊息，然後按一下 [複製訊息文字]  。  
  
5.  按一下 [偵錯]  功能表上的 [停止偵錯]  以切換到設計模式。  
  
6.  以滑鼠右鍵按一下樞紐轉換，然後按一下 [編輯]  。  
  
7.  取消核取 [忽略不相符的樞紐索引鍵值，並在 DataFlow 執行後回報]  選項，然後使用下列格式，將樞紐索引鍵值貼到 [根據值產生樞紐輸出資料行]  方塊中。  
  
     [value1],[value2],[value3]  
  
 **立即產生資料行**  
 按一下以便針對 [根據值產生樞紐輸出資料行]  方塊中列出的每個樞紐索引鍵值，建立輸出資料行。  
  
 輸出資料行會出現在 [現有的樞紐輸出資料行]  方塊中。  
  
 **現有的樞紐輸出資料行**  
 列出樞紐索引鍵值的輸出資料行  
  
 下表顯示資料在 **Year** 資料行上樞紐之前的資料集。  
  
|Year|產品名稱|總計|  
|----------|------------------|-----------|  
|2004|HL Mountain Tire|1504884.15|  
|2003|Road Tire Tube|35920.50|  
|2004|Water Bottle - 30 oz.|2805.00|  
|2002|Touring Tire|62364.225|  
  
 下表顯示資料在 **Year** 資料行上進行樞紐之後的資料集。  
  
||2002|2003|2004|  
|-|----------|----------|----------|  
|HL Mountain Tire|141164.10|446297.775|1504884.15|  
|Road Tire Tube|3592.05|35920.50|89801.25|  
|Water Bottle - 30 oz.|*NULL*|*NULL*|2805.00|  
|Touring Tire|62364.225|375051.60|1041810.00|  
  
 若要在 **Year** 資料行上樞紐資料 (如上所示)，則會在 [樞紐]  對話方塊中設定下列選項。  
  
-   年在 [樞紐索引鍵]  清單方塊中呈選取狀態。  
  
-   產品名稱在[設定索引鍵]  清單方塊中呈選取狀態。  
  
-   總計在 [樞紐值]  清單方塊中呈選取狀態。  
  
-   在 [根據值產生樞紐輸出資料行]  方塊中會輸入下列值。  
  
     [2002],[2003],[2004]  
  
## <a name="configuration-of-the-pivot-transformation"></a>設定樞紐轉換  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關 [進階編輯器]  對話方塊中可設定屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-content"></a>相關內容  
 如需如何設定此元件屬性的資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [取消樞紐轉換](../../../integration-services/data-flow/transformations/unpivot-transformation.md)   
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
