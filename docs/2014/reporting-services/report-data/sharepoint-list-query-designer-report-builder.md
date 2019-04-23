---
title: SharePoint 清單查詢設計工具 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10016"
ms.assetid: b8a3122c-8008-4950-b515-937636d7967f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7d26534094e8e21029d9836c0cad065e1a76bdd3
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59956844"
---
# <a name="sharepoint-list-query-designer-report-builder"></a>SharePoint 清單查詢設計工具 (報表產生器)
  報表產生器同時提供了圖形化查詢設計工具和以文字為基礎的查詢設計工具，可協助您建立查詢，以便指定要從 SharePoint 網站中針對報表資料集擷取的資料。 您可以使用圖形化查詢設計工具來瀏覽 SharePoint 清單中繼資料、以互動方式建立查詢以及檢視查詢的結果。 您可以使用以文字為基礎的查詢設計工具來檢視圖形化查詢設計工具所建立的查詢、修改查詢，或輸入查詢命令。 您也可以從檔案或報表匯入現有的查詢。  
  
> [!IMPORTANT]  
>  當使用者建立與執行查詢時，可以存取資料來源。 您應該授與資料來源的最小權限，例如唯讀權限。  
  
## <a name="graphical-query-designer"></a>圖形化查詢設計工具  
 在圖形化查詢設計工具中，您可以瀏覽 SharePoint 網站、以互動方式建立擷取資料集的 SharePoint 網站清單資料的命令。 您可以選擇要包含在資料集中的欄位，並選擇性地指定限制資料集中之資料的篩選。 您可以指定將篩選當做參數使用，並在執行階段提供篩選的值。  
  
 SharePoint 清單包含大量的 SharePoint 專屬欄位，在報表中不一定實用。 查詢設計工具提供隱藏這些欄位的選項，方便您更快速地決定要使用的欄位。  
  
 圖形化查詢設計工具分成三個區域  
  
-   瀏覽窗格，可在其中選取要使用的清單項目及其欄位。  
  
-   設計區域，可建立查詢。  
  
-   可以檢視查詢結果的結果窗格。  
  
 下圖顯示搭配 SharePoint 清單使用時的圖形化查詢設計工具。  
  
 ![rsQD_Relational_Graphical_SharePoint](../media/rsqd-relational-graphical-sharepoint.gif "rsQD_Relational_Graphical_SharePoint")  
  
 下表會描述各個窗格的功能。  
  
 [SharePoint 清單](#DatabaseView)  
 顯示 SharePoint 清單和清單中每個項目內的欄位。  
  
 [選取的欄位](#SelectedFields)  
 顯示來自 [SharePoint 清單] 窗格中所選取項目的 SharePoint 清單欄位名稱清單。 這些欄位會成為報表資料集的欄位集合。  
  
 [套用的篩選](#AppliedFilters)  
 針對 [資料庫檢視] 窗格中的資料表或檢視表顯示欄位和篩選準則的清單。  
  
 [查詢結果](#QueryResults)  
 針對自動產生的查詢顯示結果集的範例資料。  
  
###  <a name="DatabaseView"></a> SharePoint 清單窗格  
 [SharePoint 清單] 窗格會顯示您有權檢視之資料庫物件的中繼資料，而這個權限是由資料來源連接和認證所決定。 階層式檢視會檢視依照資料庫結構描述所組織的資料庫物件。 您可以展開每個結構描述的節點，以便檢視資料表、檢視表、預存程序和資料表值函式。 您可以展開資料表或檢視表來顯示資料行。  
  
###  <a name="SelectedFields"></a> 選取的欄位窗格  
 [選取的欄位] 窗格會顯示您為 SharePoint 清單項目選取的清單項目欄位。 顯示在這個窗格中的欄位會成為報表資料集的欄位集合。 在您建立資料集和查詢之後，請使用 [報表資料] 窗格來檢視報表資料集的欄位集合。 這些欄位代表檢視報表時，您可以在資料表、圖表和其他報表項目中顯示的資料。  
  
 若要在這個窗格中加入或移除欄位，請在 [SharePoint 清單] 窗格中選取或清除資料表或檢視欄位的核取方塊。  
  
###  <a name="AppliedFilters"></a> 套用的篩選窗格  
 [套用的篩選] 窗格會顯示用來限制在執行階段擷取之資料列數目的準則。 在這個窗格中指定的準則會用來產生 [!INCLUDE[tsql](../../includes/tsql-md.md)] WHERE 子句。 當您選取參數選項時，就會自動建立報表參數。 以查詢參數為基礎的報表參數可讓使用者指定查詢的值，以便控制報表中的資料。  
  
 系統會顯示下列資料行：  
  
-   **欄位名稱** ：顯示要套用準則的欄位名稱。  
  
-   **運算子** ：顯示要在篩選運算式中使用的運算。  
  
-   **值** ：顯示要在篩選運算式中使用的值。  
  
-   **參數** ：顯示要將查詢參數加入至查詢的選項。 您可以使用資料集屬性來檢視查詢參數與報表參數之間的關聯性。  
  
###  <a name="QueryResults"></a> 查詢結果窗格  
 [查詢結果] 窗格會針對其他窗格中之選取項目所指定的自動產生查詢顯示結果。 結果集中的資料行就是您在 [選取的欄位] 窗格中指定的欄位，而且資料列資料是由您在 [套用的篩選] 窗格中指定的篩選所限制。  
  
 這項資料代表您執行查詢時來自資料來源的值。 這項資料不會儲存在報表定義中。報表中的實際資料是在處理報表時擷取的。  
  
 從資料來源中擷取資料的順序會決定結果集中的排序次序。 不過，您可以透過修改查詢，或在擷取報表的資料之後，變更排序次序。  
  
### <a name="graphical-query-designer-toolbar"></a>圖形化查詢設計工具工具列  
 關聯式查詢設計工具的工具列會提供下列按鈕來協助您指定或檢視查詢的結果。  
  
|按鈕|描述|  
|------------|-----------------|  
|**當成文字編輯**|切換至以文字為基礎的查詢設計工具，以便檢視自動產生的查詢，或是修改查詢。|  
|**匯入**|從檔案或報表匯入現有的查詢。 支援 .sql 和 .rdl 檔案類型。|  
|**執行查詢**|執行查詢。 [查詢結果] 窗格會顯示結果集。|  
|**顯示隱藏的欄位**|切換顯示或隱藏 SharePoint 自動產生，但通常不會在報表中使用的欄位，例如 SharePoint 連結項目的 [ProgId] 和 [Level]。 隱藏這些欄位會縮短欄位清單，且更方便使用。|  
  
## <a name="see-also"></a>另請參閱  
 [查詢設計工具 &#40;報表產生器&#41;](../query-designers-report-builder.md)  
  
  
