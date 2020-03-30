---
title: Tablix 資料區 (報表產生器) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 99f83b32-4b86-4d40-973c-9a328d23ac8b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a37105db6639b7d7db35c3beb1fc85020015d7e4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081366"
---
# <a name="tablix-data-region-report-builder-and-ssrs"></a>Tablix 資料區 (報表產生器及 SSRS)
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]中，Tablix 資料區是一種廣義的配置報表項目，可在組織到資料列和資料行的資料格中顯示分頁報表資料。 報表資料可以是從資料來源擷取時的詳細資料，或者是組織到您指定之群組中的彙總詳細資料。 每個 Tablix 資料格可以包含任何報表項目，例如文字方塊或影像，或是其他資料區，例如 Tablix 區、圖表或量測計。 若要將多個報表項目加入至資料格，請先加入當做容器使用的矩形。 然後再將報表項目加入至矩形。  
  
 資料表、矩陣和清單資料區域會以基礎 Tablix 資料區的範本在功能區上表示。 當您將其中一個範本加入到報表時，實際上是加入針對特定資料配置最佳化的 Tablix 資料區。 根據預設，資料表範本會以格線配置顯示詳細資料、矩陣會以格線配置顯示群組資料，而清單則會以自由形式的配置顯示詳細資料。  
  
 依預設，資料表或矩陣中的每個 Tablix 資料格都包含一個文字方塊。 清單中的資料格則包含一個矩形。 您可以將預設的報表項目取代成不同的報表項目，例如影像。  
  
 當您定義資料表、矩陣或清單的群組時，報表產生器和報表設計師會將資料列和資料行加入到顯示群組資料的 Tablix 資料區。  
  
 若要了解 Tablix 資料區，您必須先了解下列事項：  
  
*   詳細資料與群組資料之間的差異。  
  
*   群組在當做資料列群組的水平軸以及在當做資料行群組的垂直軸上，會組織成群組階層的成員。  
  
*  Tablix 資料格在下列四個 Tablix 資料區中的用途：主體、資料列群組首、資料行群組首以及邊角。  
  
*  靜態和動態的資料列與資料行，以及與群組之間的關聯性。  
  
 本文詳細說明這些概念，以說明當您加入範本及建立群組時，報表產生器和報表設計師所為您加入的結構，讓您能夠修改結構以符合您自己的需求。 報表產生器和報表設計師會提供多個視覺指標以協助您辨識 Tablix 資料區結構。 如需詳細資訊，請參閱 [Tablix 資料區資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-detail-and-grouped-data"></a>了解詳細資料與群組資料  
 詳細資料是來自報表資料集的所有資料，因為它來自資料來源。 詳細資料實際上是執行資料集查詢時，您在查詢設計工具結果窗格中看到的內容。 實際詳細資料包括您所建立的導出欄位，而且會受限於資料集、資料區域與詳細資料群組上設定的篩選。 您可以使用 [Quantity] 之類的簡單運算式來顯示詳細資料列上的詳細資料。 報表執行時，詳細資料列在執行階段會針對查詢結果中的每個資料列重複一次。  
  
 群組資料是由您在群組定義 (例如，[SalesOrder]) 中指定之值所組織的詳細資料。 您可以使用彙總群組資料的運算式 (例如，[Sum(Quantity)]) 來顯示群組資料列和資料行上的群組資料。 如需詳細資訊，請參閱[了解群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
## <a name="understanding-group-hierarchies"></a>了解群組階層  
 群組會組織為群組階層的成員。 資料列群組和資料行群組階層是不同軸上的相同結構。 將資料列群組向頁面下方展開，並將資料行群組跨頁面展開。  
  
 樹狀結構表示擁有父子式關聯性的巢狀資料列和資料行群組，例如，包含子類別目錄的類別目錄。 父群組是樹狀結構的根，而子群組則是其分支。 群組也可以有獨立、相鄰的關聯性，例如，依領域銷售和依年份銷售。 多個不相關的樹狀階層稱為樹系。 在 Tablix 資料區中，資料列群組和資料行群組會分別以獨立的樹系表示。 如需詳細資訊，請參閱[了解群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)。  
  
## <a name="understanding-tablix-data-region-areas"></a>了解 Tablix 資料區的區域  
 Tablix 資料區具有四個可能的資料格區域：Tablix 邊角、Tablix 資料列群組階層、Tablix 資料行群組階層或 Tablix 主體。 Tablix 主體永遠存在。 其他區域是選擇性的。  
  
 Tablix 主體區域中的資料格會顯示詳細資料和群組資料。  
  
 資料列群組區域中的資料格會在建立資料列群組時自動建立。 根據預設，這些是資料列群組首資料格，而且會顯示資料列群組執行個體值。 例如，當您依 [SalesOrder] 分組時，群組執行個體值是您分組所依據的個別銷售訂單。  
  
 資料行群組區域中的資料格會在建立資料行群組時自動建立。 根據預設，這些是資料行群組首資料格，而且會顯示資料行群組執行個體值。 例如，當您依 [Year] 分組時，群組執行個體值是您分組所依據的個別年份。  
  
 Tablix 邊角區域中的資料格會在您已經定義資料列群組和資料行群組時自動建立。 此區域中的資料格可以顯示標籤，或者您可以合併資料格並建立標題。  
  
 如需詳細資訊，請參閱 [Tablix 資料區的區域 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md)。  
  
## <a name="understanding-static-and-dynamic-rows-and-columns"></a>了解靜態和動態的資料列與資料行  
 Tablix 資料區會將資料格組織到與群組相關聯的資料列和資料行中。 資料列群組和資料行的群組結構相同。 此範例使用資料列群組，但是您可以套用相同的概念至資料行群組。  
  
 資料列是靜態或動態的。 靜態資料列與群組沒有關聯。 當報表執行時，靜態資料列會轉譯一次。 資料表頁首及頁尾是靜態資料列。 靜態資料列會顯示標籤和總計。 靜態資料列中的資料格範圍為資料區。  
  
 動態資料列與一個或多個群組相關聯。 動態資料列會針對最內部群組的每個唯一群組值轉譯一次。 動態資料列中的資料格範圍是資料格所屬的最內部資料列群組及資料行群組。  
  
 動態詳細資料列與您將資料表或清單加入到設計介面時自動建立的詳細資料群組相關聯。 根據定義，詳細資料群組是 Tablix 資料區最內部的群組。 詳細資料列中的資料格會顯示詳細資料。  
  
 當您將資料列群組或資料行群組加入到現有的 Tablix 資料區時，會建立動態群組資料列。 動態群組資料列中的資料格會顯示預設範圍的彙總值。  
  
 [加入總計] 功能會自動在目前群組的外部建立資料列，您可以在該群組上顯示群組範圍的值。 您也可以手動加入靜態和動態資料列。 視覺指標可協助您了解哪些資料列是靜態的，以及哪些資料列是動態的。 如需詳細資訊，請參閱 [Tablix 資料區資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [將多個資料區連結至相同的資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [控制報表頁面上的 Tablix 資料區顯示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)   
 [探索 Tablix 資料區的彈性 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
