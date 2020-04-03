---
title: 匯出至 XML (報表產生器) | Microsoft Docs
description: 在報表產生器中，XML 轉譯延伸模組會將分頁報表轉譯為 XML 格式。 將 XML 匯入至資料庫、作為訊息使用，或傳送至應用程式。
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 11d72068-2d97-495e-948f-12d1e8c1957d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 71e3b5102fa1ff37e7cea22562919b202889ecc3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "80342831"
---
# <a name="exporting-to-xml-report-builder-and-ssrs"></a>匯出至 XML (報表產生器及 SSRS)
  XML 轉譯延伸模組會傳回 XML 格式的分頁報表。 報表 XML 的結構描述為報表特有的，且僅包含資料。 XML 轉譯延伸模組不會轉譯配置資訊，也不會維持分頁。 此延伸模組所產生的 XML 可以匯入資料庫中 (當做 XML 資料訊息使用)，或傳送到自訂應用程式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="report-items"></a><a name="ReportItems"></a> 報表項目  
 下表描述報表項目轉譯的方式。  
  
|Item|轉譯行為|  
|----------|------------------------|  
|Report|轉譯成 XML 文件的最上層元素。|  
|資料區域|轉譯成元素中的元素做為其容器。 資料區包含資料表、矩陣和清單，可將資料顯示為文字和圖表、資料橫條、走勢圖、量測計，以及將資料視覺化的指標。|  
|群組和詳細資料區段|每一個執行個體會轉譯成元素中的元素做為其容器。|  
|文字方塊|轉譯成其容器中的屬性或元素。|  
|矩形|轉譯成其容器中的元素。|  
|矩陣資料行群組|轉譯成資料列群組中的元素。|  
|對應|轉譯成元素中的元素做為其容器。 地圖圖層是地圖的子元素，每一個地圖圖層都包含其地圖成員的元素和地圖成員屬性。|  
|圖表|轉譯成元素中的元素做為其容器。 數列是圖表的子元素，而類別目錄是數列的子元素。 轉譯每個圖表值的所有圖表標籤。 標籤和值都會當做屬性加入。|  
|資料橫條|轉譯成元素中的元素做為其容器，類似圖表。 資料橫條通常不包含階層或標籤，只包含值。|  
|走勢圖|轉譯成元素中的元素做為其容器，類似圖表。 走勢圖通常不包含階層或標籤，只包含值。|  
|量測計|轉譯成元素中的元素做為其容器。 以標尺的最小值與最大值、範圍的開始值與結束值，以及指標的值當做屬性轉譯為單一元素。|  
|指標|轉譯成元素中的元素做為其容器，類似量測計。 以作用中的狀態名稱、可用的狀態以及資料值當做屬性，轉譯成單一元素。|  
  
 使用 XML 轉譯延伸模組轉譯的報表也遵從下列規則：  
  
-   XML 元素和屬性會依其顯示在報表定義中的順序轉譯。  
  
-   會忽略分頁。  
  
-   不會轉譯頁首和頁尾。  
  
-   不會轉譯無法透過切換使其顯示的隱藏項目。 會轉譯一開始可見的項目和可透過切換使其可見的隱藏項目。  
  
-   **Images, lines, and custom report items** 都會忽略。  
  
  
##  <a name="data-types"></a><a name="DataTypes"></a> 資料型別  
 文字方塊元素或屬性會根據文字方塊所顯示的值，指派 XSD 資料類型。  
  
|如果所有文字方塊值為|指派的資料類型為|  
|--------------------------------|---------------------------|  
|**Int16**、 **Int32**、 **Int64**、 **UInt16**、 **UInt32**、 **UInt64**、 **Byte**、 **SByte**|**xsd:integer**|  
|**十進位** (或 **十進位** 和任何整數或位元組資料類型)|**xsd:decimal**|  
|**浮點數** (或 **十進位** 和任何整數或位元組資料類型)|**xsd:float**|  
|**雙精度** (或 **十進位** 和任何整數或位元組資料類型)|**xsd:double**|  
|**DateTime 或 DateTime Offset**|**xsd:dateTime**|  
|**Time**|**xsd:string**|  
|**布林值**|**xsd:boolean**|  
|**String**、 **Char**|**xsd:string**|  
|其他|**xsd:string**|  
  
  
##  <a name="xml-specific-rendering-rules"></a><a name="XMLSpecificRenderingRules"></a> XML 特定的轉譯規則  
 下列幾節描述 XML 轉譯延伸模組如何解譯報表中的項目。  
  
### <a name="report-body"></a>報表主體  
 報表會轉譯為 XML 文件的根元素。 元素的名稱來自於 [屬性] 窗格中設定的 DataElementName 屬性。  
  
 XML 命名空間定義與結構描述參考屬性也包含在報表元素中 變數會以粗體類型顯示：  
  
 <**Report** xmlns="**SchemaName**" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xsi:**schemaLocation**="**SchemaNameReportURL**&amp;rc%3aSchema=true" Name="ReportName">  
  
 變數的值如下：  
  
|名稱|值|  
|----------|-----------|  
|Report|Report.DataElementName|  
|ReportURL|伺服器上，報表的 URLEncoded 絕對 URL。|  
|SchemaName|Report.SchemaName. 如果為 null，則是 Report.Name。 如果使用 Report.Name，會先以 XmlConvert.EncodeLocalName 編碼。|  
|ReportName|報表的名稱。|  
  
### <a name="text-boxes"></a>文字方塊  
 文字方塊會依據 DataElementStyle RDL 屬性 (property) 而轉譯成元素或屬性 (attribute)。 元素或屬性 (attribute) 的名稱來自於 TextBox.DataElementName RDL 屬性 (property)。  
  
### <a name="charts-data-bars-and-sparklines"></a>圖表、資料橫條和走勢圖  
 圖表、資料橫條和走勢圖都會以 XML 轉譯。 資料是有結構的。  
  
### <a name="gauges-and-indicators"></a>量測計與指標  
 量測計與指標都會以 XML 轉譯。 資料是有結構的。  
  
### <a name="subreports"></a>子報表  
 子報表會轉譯成元素。 元素名稱擷取自 DataElementName RDL 屬性。 報表的 TextBoxesAsElements 屬性設定會覆寫子報表的這個設定。 命名空間與 XSLT 屬性不會加入到子報表元素中。  
  
### <a name="rectangles"></a>矩形  
 矩形會轉譯成元素。 元素名稱擷取自 DataElementName RDL 屬性。  
  
### <a name="custom-report-items"></a>自訂報表項目  
 轉譯延伸模組看不到 CustomReportItems (CRI)。 如果報表中有自訂報表項目，轉譯延伸模組會將其轉譯為傳統的報表項目。  
  
### <a name="images"></a>影像  
 不會轉譯影像。  
  
### <a name="lines"></a>線條  
 不會轉譯線條。  
  
  
### <a name="tables-matrices-and-lists"></a>資料表、矩陣和清單  
 資料表、矩陣和清單會轉譯成元素。 元素的名稱來自於 Tablix DataElementName RDL 屬性。  
  
#### <a name="rows-and-columns"></a>資料列與資料行  
 資料行會在資料列中轉譯。  
  
#### <a name="tablix-corner"></a>Tablix 邊角  
 不會轉譯邊角。 只會轉譯邊角的內容。  
  
#### <a name="tablix-cells"></a>Tablix 資料格  
 Tablix 資料格會轉譯成元素。 項目名稱擷取自儲存格的 DataElementName RDL 屬性。  
  
#### <a name="automatic-subtotals"></a>自動小計  
 不會轉譯 Tablix 自動小計。  
  
#### <a name="row-and-column-items-that-do-not-repeat-with-a-group"></a>群組內沒有重複的資料列與資料行項目  
 群組內沒有重複的項目 (例如，標籤、小計和總計) 會轉譯為元素。 元素的名稱來自於 TablixMember.DataElementName RDL 屬性。  
  
 TablixMember.DataElementOutput RDL 屬性控制是否要轉譯非重複的項目。  
  
 如果沒有提供 Tablix 成員的 DataElementName 屬性，系統會以下列格式動態產生非重複項目的名稱：  
  
 RowX：對於非重複的資料列，其中的 X 在目前的父系中是以零為基礎的資料列索引。  
  
 ColumnY：對於非重複的資料行，其中的 Y 在目前的父系中是以零為基礎的資料行索引。  
  
 非重複的標頭會轉譯為群組內沒有重複之資料列或資料行的子系。  
  
 如果非重複的成員沒有對應的 Tablix 資料格，就不會被轉譯。 如果是跨越一個以上資料行的 Tablix 資料格，可能會發生這個狀況。  
  
#### <a name="rows-and-columns-that-repeat-with-a-group"></a>群組內重複的資料列與資料行  
 群組內重複的資料列與資料行會根據 Tablix.DataElementOutput 規則來轉譯。 元素名稱擷取自 DataElementName 屬性。  
  
 群組內每個唯一的值都會轉譯為群組的子元素。 元素名稱擷取自 Group.DataElementName 屬性。  
  
 如果 DataElementOutput 屬性值等於「輸出」，重複項目的標頭就會轉譯為詳細資料元素的子系。  
  
  
##  <a name="custom-formats-and-xsl-transformations"></a><a name="CustomFormatsXSLTransformations"></a> 自訂格式和 XSL 轉換  
 使用 XSL 轉換 (XSLT)，幾乎可以將 XML 轉譯延伸模組所產生的 XML 檔案轉換成任何格式。 此功能可用來產生現有的轉譯延伸模組已不支援的資料格式。 在嘗試建立您自己的轉譯延伸模組之前，請考慮使用 XML 轉譯延伸模組和 XSLT。  
  
  
##  <a name="duplicate-names"></a><a name="DuplicateName"></a> 重複的名稱  
 如果在相同的範圍內有重複的資料元素名稱，轉譯器會顯示一個錯誤訊息。  
  
  
##  <a name="xslt-transformations"></a><a name="XSLTTransformations"></a> XSLT 轉換  
 XML 轉譯器可以將伺服器端的 XSLT 轉換套用到原始 XML 資料。 套用 XSLT 時，轉譯器會輸出轉換的內容，而非輸出 XML 原始資料。 轉換會在伺服器上，而非用戶端上進行。  
  
 系統會在報表定義檔案中，以報表的 DataTransform 屬性或以 XSLT *DeviceInfo* 參數，定義要套用到輸出的 XSLT。 如果設定其中一個值，就會在每次使用 XML 轉換器時進行轉換。 使用訂閱時，必須在 RDL DataTransform 屬性中定義 XSLT。  
  
 如果有同時透過 DataTransform 定義屬性和裝置資訊設定指定 XSLT 檔案，會先出現在 DataTransform 中指定的 XSLT，接著出現由裝置資訊設定所設定的 XSLT。  
  
  
###  <a name="device-information-settings"></a><a name="DeviceInfo"></a> 裝置資訊設定  
 您可以變更此轉譯器的某些預設值，方法是，變更裝置資訊設定，包括：  
  
-   套用至 XML 的轉換 (XSLT)。  
  
-   XML 文件的 MIME 類型。  
  
-   是否套用格式字串至資料。  
  
-   是否縮排 XML 輸出。  
  
-   是否包含 XML 結構描述名稱。  
  
-   XML 文件的編碼。  
  
-   XML 文件的副檔名。  
  
 如需詳細資訊，請參閱＜ [XML Device Information Settings](../../reporting-services/xml-device-information-settings.md)＞。  
  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同報表轉譯延伸模組的互動式功能 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [轉譯報表項目 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
