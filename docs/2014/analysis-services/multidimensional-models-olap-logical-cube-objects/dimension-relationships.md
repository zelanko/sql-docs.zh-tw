---
title: 維度關聯性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- relationships [Analysis Services]
- member groups [Analysis Services]
- regular dimensions [Analysis Services]
- many-to-many relationships [Analysis Services]
- cubes [Analysis Services], relationships
- reference dimensions
- dimensions [Analysis Services], relationships
- fact dimensions [Analysis Services]
- relationships [Analysis Services], dimensions
ms.assetid: de54c059-cb0f-4f66-bd70-8605af05ec4f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1fe1521f2eebaa4413b49c315f17a6b1b6a5914
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/25/2019
ms.locfileid: "68887933"
---
# <a name="dimension-relationships"></a>維度關聯性
  維度使用方式會定義 Cube 維度和 Cube 內量值群組之間的關聯性。 Cube 維度是在特定 Cube 中使用之資料庫維度的執行個體。 Cube 可以，而且經常會，具有與量值群組沒有直接關聯的 Cube 維度，但可能會透過其他維度或量值群組，間接地與此量值群組相關。 當您將資料庫維度或量值群組加入至 cube 時[!INCLUDE[msCoName](../../includes/msconame-md.md)] ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]會嘗試藉由檢查 cube 的資料來源視圖中的維度資料表與事實資料表之間的關聯性，以及檢查，來判斷維度的使用方式。維度中屬性之間的關聯性。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會自動設定其可偵測到之關聯性的維度使用方式設定。  
  
 維度與量值群組之間的關聯性，是由維度和參與關聯性的事實資料表所組成的，而資料粒度屬性則會指定特定量值群組中之維度的資料粒度。  
  
## <a name="regular-dimension-relationships"></a>一般維度關聯性  
 當維度的索引鍵資料行直接聯結到事實資料表時，在 Cube 維度與量值群組之間會存在一般維度關聯性。 這個直接關聯性是以基礎關係資料庫中的主鍵-外鍵關聯性為依據，但也可能是以資料來源視圖中所定義的邏輯關聯性為基礎。 一般維度關聯性代表在傳統星狀結構描述設計中，維度資料表與事實資料表之間的關聯性。 如需一般關聯性的詳細資訊，請參閱[定義一般關聯性和一般關聯性屬性](../multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md)。  
  
## <a name="reference-dimension-relationships"></a>參考維度關聯性  
 當維度的索引鍵資料行透過其他維度資料表中的索引鍵間接聯結到事實資料表時，Cube 維度與量值群組之間就會有參考維度關聯性 (如下圖所示)。  
  
 ![邏輯圖表, 參考的維度關聯性](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension1.gif "邏輯圖表, 參考的維度關聯")性  
  
 參考維度關聯性代表在雪花式結構描述設計中，維度資料表與事實資料表之間的關聯性。 當您在雪花式結構描述中連接維度資料表時，可以使用多份資料表中的資料行來定義單一維度；或者根據不同的維度資料表來定義個別的維度，然後使用參考維度關聯性設定來定義這些維度之間的連結。 下圖顯示一個名為**InternetSales**的事實資料表，以及一個雪花式架構中名為**Customer**和**Geography**的兩個維度資料表。  
  
 ![邏輯架構，參考的維度關聯]性(https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdim-schema1.gif "邏輯架構，參考的維度關聯")性  
  
 您可以使用**Customer**資料表做為維度主資料表，並將**Geography**資料表當做相關資料表來建立維度。 接著，在維度和 InternetSales 量值群組之間定義一般關聯性。  
  
 或者，您可以建立兩個與 InternetSales 量值群組相關的維度：以**Customer**資料表為基礎的維度，以及以**Geography**資料表為基礎的維度。 然後您就可以利用 Customer 維度，使用參考維度關聯性將 Geography 維度關聯至 InternetSales 量值群組。 在此情況下，當依 Geography 維度來標示 InternetSales 量值群組之事實的維度時，會依客戶與依地理位置來標示事實的維度。 如果 Cube 包含稱為 Reseller Sales 的第二個量值群組，則因為 Reseller Sales 與 Geography 之間並沒有關聯性，所以您將無法在 Reseller Sales 量值群組中依 Geography 來標示事實的維度。  
  
 可鏈結在一起的參考維度數目不限，如下圖所示。  
  
 ![邏輯圖表, 參考的維度關聯性](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension2.gif "邏輯圖表, 參考的維度關聯")性  
  
 如需參考關聯性的詳細資訊，請參閱[定義參考的關聯性和參考的關聯性屬性](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)。  
  
## <a name="fact-dimension-relationships"></a>事實維度關聯性  
 事實維度 (一般稱為變質維度) 是從事實資料表內的屬性資料行 (而非從維度資料表內的屬性資料行) 建構而來的標準維度。 有時候會將有用的維度資料儲存在事實資料表中，以減少資料的重複。 例如，下圖顯示[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]範例資料庫中的**FactResellerSales**事實資料表。  
  
 ![事實資料表中的資料行可以支援維度](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-factdim.gif "事實資料表中的資料行可以支援維度")  
  
 此資料表所包含的屬性資訊，不但有零售商所發出的訂單產品線，還有關於訂單本身的資訊。 上圖中所圈出的屬性會識別**FactResellerSales**資料表中可用來當做維度屬性的資訊。 在此情況下，還有另外兩項資訊，即轉售商發出的貨運追蹤編號和訂單號碼，是由 CarrierTrackingNumber 和 CustomerPONumber 屬性資料行來表示。 這項資訊很有趣-例如，使用者對於在單一追蹤號碼下出貨的所有訂單，一定會有興趣查看匯總資訊，例如產品成本總計。 但沒有維度，也無法組織或彙總這兩個屬性的資料。  
  
 理論上，您可以建立與 FactResellerSales 資料表使用相同索引鍵資訊的維度資料表，並將其他兩個屬性資料行 (CarrierTrackingNumber 和 CustomerPONumber) 移到該維度資料表。 不過，這樣做會重複大量資料，並在資料倉儲中增加了不必要的複雜性，而這一切只為了以個別維度來表示兩個屬性。  
  
> [!NOTE]  
>  事實資料表經常會用來支援鑽研動作。 如需動作的詳細資訊，請參閱[動作 &#40;Analysis Services - 多維度資料&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)。  
  
> [!NOTE]  
>  在每次更新事實關聯性所參考的量值群組之後，都必須以累加方式更新事實維度。 如果事實維度是 ROLAP 維度，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理引擎會卸除任何快取，並以累加方式處理量值群組。  
  
 如需事實關聯性的詳細資訊，請參閱[定義事實關聯性和事實關聯性屬性](../multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)。  
  
## <a name="many-to-many-dimension-relationships"></a>多對多維度關聯性  
 在大部分維度中，每一個事實只會聯結到一個維度成員，且單一維度成員可與多個事實相關聯。 在關聯式資料庫詞彙中，這稱為「一對多關聯性」。 然而，將單一事實聯結至多個維度成員，是很有用的。 例如，銀行客戶可以有多個帳戶 (支票、儲蓄、信用卡和投資帳戶)，而一個帳戶可以有聯合或多個擁有者。 從這樣的關聯性建構的客戶維度，就會有多個與單一帳戶交易相關的成員。  
  
 ![邏輯架構/多對多維度關聯]性(https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-many-dimension1.gif "邏輯架構/多對多維度關聯")性  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可讓您定義維度與事實資料表之間的多對多關聯性。  
  
> [!NOTE]  
>  若要支援多對多維度關聯性，資料來源檢視必須在所有相關資料表之間建立外部索引鍵關聯性 (如上圖所示)。 否則，當您在 [維度設計師] 的 [**維度使用**方式] 索引標籤中建立關聯性時，將無法選取正確的中繼量值群組。  
  
 如需多對多關聯性的詳細資訊，請參閱[定義多對多關聯性和多對多關聯性屬性](../multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [維度 &#40;Analysis Services - 多維度資料&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
