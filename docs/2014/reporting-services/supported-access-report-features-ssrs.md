---
title: 支援的 Access 報表功能 (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], Access reports
- functions [Reporting Services]
- controls [Reporting Services]
- Access reports [Reporting Services]
- properties [Reporting Services], Access reports
- importing reports
- modules [Reporting Services]
ms.assetid: 7ffec331-6365-4c13-8e58-b77a48cffb44
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ae982257f0be29103803a7d036142f58a50f1a04
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631329"
---
# <a name="supported-access-report-features-ssrs"></a>支援的 Access 報表功能 (SSRS)
  當您將報表匯入報表設計師時，匯入程序會將 [!INCLUDE[msCoName](../includes/msconame-md.md)] Access 報表轉換成 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表定義語言 (RDL) 檔案。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援多種 Access 的功能；但因為 Access 及 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 之間的差異，會稍微修改或不支援某些項目。 此主題描述 Access 報表功能如何轉換成 RDL。  
  
## <a name="importing-access-reports"></a>匯入 Access 報表  
 部分查詢包含 Access 特有的程式碼。 Access 程式碼不會隨報表一起匯入。 同時，如果查詢中包含內嵌字串，就可能無法正確匯入報表。 若要修正，請以字元碼取代字串。 例如，請以 CHAR(34) 取代逗號 (,)。  
  
 匯入程序不會正確傳遞分號 （;） 或 XML 標記字元 (\<、 > 等等) 中的連接字串資訊。 如果連接字串中包含分號或 XML 標記字元，您必須在報表匯入之後，在新的報表中手動設定密碼。  
  
 匯入程序不會匯入連接字串中的連接或一般逾時設定。 您可能需要在報表匯入之後，再調整這些設定。  
  
 如果您匯入的報表有包含查詢參數的查詢，當報表匯入時，將不會轉換此查詢。 若要隨著報表匯入查詢，請暫時將 Access 報表的查詢參數取代成硬式編碼值，然後在報表匯入後，再將硬式編碼值取代成查詢參數。  
  
## <a name="page-layout"></a>頁面配置  
 Access 的頁面配置與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的頁面配置不同。 Access 會使用「帶狀」的方式在頁面上排列項目，也就是在頁面上垂直排列區段。 這些區段可能包含報表頁首、報表頁尾、頁首、頁尾、群組及詳細資料。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 可提供更彈性的配置。 資料區提供群組及詳細資料，而且您可以在報表主體的任意位置放置 (甚至並排) 多個資料區域。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 也包含「帶狀」的頁首及頁尾，與 Access 中的頁首及頁尾類似。  
  
 從 Access 匯入報表至報表設計師時，Access 報表中的頁首和頁尾會轉換成 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表的頁首和頁尾。 群組和詳細資料會轉換成清單資料區域。 報表首和報表尾會放入報表的主體，而非個別的帶狀位置。 這可能會造成項目的位置與在 Access 報表中的位置有些不同。  
  
> [!NOTE]  
>  在部份 Access 報表中，相鄰的報表項目實際上可能會重疊。 當您使用報表設計師匯入報表時，不會修正此重疊，而在執行報表時可能導致無法預期的結果。  
  
## <a name="data-sources"></a>資料來源  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援 OLE DB 資料來源，例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 如果從 Access 專案 (.adp) 檔案匯入報表，資料來源的連接字串會從 .adp 檔案的連接字串取得。 如果從 Access 資料庫 (.mdb 或 .accdb) 檔案匯入報表，連接字串可能會指向 Access 資料庫，因此您可能必須在報表匯入後更正它。 如果 Access 報表的資料來源是查詢，查詢資訊會不經修改地直接儲存到 RDL。 如果 Access 報表的資料來源是資料表，轉換程序會根據該資料表名稱和資料表中的欄位建立查詢。  
  
## <a name="reports-with-custom-modules"></a>包含自訂模組的報表  
 如果沒有自訂[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vbprvb](../includes/vbprvb-md.md)]模組內包含的程式碼則不會轉換。 如果報表設計師匯入程序中遇到程式碼，會產生警告，並顯示在**工作清單**視窗。  
  
## <a name="report-controls"></a>報表控制項  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列 Access 控制項，且會將它們包含於轉換的報表定義中。  
  
|||||  
|-|-|-|-|  
|Image|ThisAddIn|線條|矩形|  
|SubForm|SubReport<br /><br /> **請注意**當 SubReport 控制項在主報表內轉換、 子報表本身會個別轉換。|TextBox||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列控制項：  
  
|||||  
|-|-|-|-|  
|BoundObjectFrame|CheckBox|ComboBox|CommandButton|  
|CustomControl|ListBox|ObjectFrame|OptionButton|  
|TabControl|ToggleButton|||  
  
 報表設計師中遇到這些控制項在匯入程序期間，如果會產生警告，並顯示在**工作清單**視窗。  
  
 其他控制項 (例如 ActiveX 和 Office Web 元件) 不會匯入。 例如，如果 Access 報表包含 OWC 圖表控制項，匯入報表時，將不會轉換此控制項。  
  
## <a name="report-properties"></a>報表屬性  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列屬性，這些屬性可以透過 Access 的使用者介面使用。 僅供程式碼使用的屬性並不受支援，因此將不列於此處。  
  
|||||  
|-|-|-|-|  
|BackColor|BackStyle|BorderColor|BorderStyle|  
|BorderWidth|BottomMargin|CanGrow (textbox)|CanShrink (textbox)|  
|Caption|FontBold|FontItalic|FontName|  
|FontSize|FontUnderline|FontWeight|ForceNewPage|  
|ForeColor|高度|HideDuplicates|超連結|  
|IsHyperlink|IsVisible|KeepTogether (group)|Left|  
|LeftMargin|LineSlant|LineSpacing|LinkChildFields|  
|LinkMasterFields|NewRowOrCol|PageFooter|PageHeader|  
|頁面|Picture|PictureTiling (report)|ReadingOrder|  
|RepeatSection|RightMargin|RunningSum|SizeMode|  
|TextAlign|頂端|TopMargin|寬度|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列屬性，這些屬性可以透過 Access 的使用者介面使用。  
  
|||||  
|-|-|-|-|  
|CanGrow (section)|CanShrink (section)|DecimalPlaces|FastLaserPrinting|  
|篩選|FilterOn|格式|FormatConditions|  
|GrpKeepTogether|KeepTogether (section)|NumeralShapes|Orientation|  
|PaintPalette|PaletteSource|PictureAlignment|PicturePages|  
|PictureSizeMode|PictureTiling (image)|ScrollBars|SpecialEffect|  
|垂直||||  
  
## <a name="grouping"></a>群組  
 Access 會使用下列三種屬性的組合來定義群組層次：群組運算式、`GroupOn` 屬性和 `GroupInterval` 屬性。 沒有群組首或群組尾的群組，會與包含在其中的群組合併。 如果群組沒有包含其他群組，便會對詳細資料區段套用排序，並卸除群組。  
  
## <a name="expressions"></a>運算式  
 Access 會使用運算式，來指定顯示在文字方塊中的值。 Access 會使用 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，加上一些彙總函式，做為運算式語言。 報表設計師會將這些 Access 運算式轉換成報表運算式。  
  
### <a name="functions"></a>函式  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表定義使用 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET 做為其原生的運算式語言，而 Access 2002 則使用 Visual Basic。 下列清單描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援的函數。  
  
#### <a name="array-functions"></a>陣列函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列陣列函數：  
  
-   LBound  
  
-   UBound  
  
#### <a name="conversion-functions"></a>轉換函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列轉換函數。  
  
|||||  
|-|-|-|-|  
|Asc|CBool|CByte|CCur|  
|CDate|CDbl|CDec|Chr|  
|Chr$|CInt|CLng|CSng|  
|CStr|CVar|CVDate|格式|  
|FormatCurrency|FormatDateTime|FormatNumber|FormatPercent|  
|Hex|Hex$|Nz|Oct|  
|Oct$|Str|Str$|StrConv|  
|Val||||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列轉換函數：  
  
-   GUIDFromString  
  
-   StringFromGUID  
  
#### <a name="database-functions"></a>資料庫函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列資料庫函數。  
  
|||||  
|-|-|-|-|  
|CreateReport|GetObject|HyperlinkPart|資料分割|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列資料庫函數。  
  
|||||  
|-|-|-|-|  
|CodeDb|CreateControl|CreateForm|CreateGroupLevel|  
|CreateObject|CreateReportControl|CurrentDb|CurrentUser|  
|DeleteControl|DeleteReportControl|Eval|IMEStatus|  
|SysCmd||||  
  
#### <a name="datetime-functions"></a>日期/時間函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列日期/時間函數。  
  
|||||  
|-|-|-|-|  
|date|Date$|DateAdd|DateDiff|  
|DatePart|DateSerial|DateValue|Day|  
|Hour|Minute|Month|MonthName|  
|現在|第二個|Time|Time$|  
|Timer|TimeSerial|TimeValue|Weekday|  
|WeekdayName|Year|||  
  
#### <a name="ddeole-functions"></a>DDE/OLE 函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列 DDE/OLE 函數。  
  
|||||  
|-|-|-|-|  
|DDE|DDEIntitate|DDERequest|DDESend|  
|LoadPicture||||  
  
#### <a name="domain-aggregate-functions"></a>網域彙總函式  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列網域彙總函式。  
  
|||||  
|-|-|-|-|  
|DAvg|DCount|DFirst|DLast|  
|DLookup|DMax|DMin|DStDev|  
|DStDevP|DSum|DVar|DVarP|  
  
#### <a name="error-handling-functions"></a>錯誤處理函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列錯誤處理函數。  
  
|||||  
|-|-|-|-|  
|Err|錯誤|Error$|IsError|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列錯誤處理函數：  
  
-   CVErr  
  
#### <a name="financial-functions"></a>財務函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列財務函數。  
  
|||||  
|-|-|-|-|  
|DDB|FV|IPmt|IRR|  
|MIRR|NPer|NPV|Pmt|  
|PPmt|PV|Rate|SLN|  
|SYD||||  
  
#### <a name="interaction-functions"></a>互動函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列互動函數。  
  
|||||  
|-|-|-|-|  
|命令|Command$|CurDir|CurDir$|  
|DeleteSetting|Dir|Dir$|Environ|  
|Environ$|EOF|FileAttr|FileDateTime|  
|FileLen|FreeFile|GetAllSettings|GetAttr|  
|GetSetting|Loc|LOF|QBColor|  
|RGB|SaveSetting|Seek|SetAttr|  
|Shell|Spc|索引標籤||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列互動函數。  
  
|||||  
|-|-|-|-|  
|DoEvents|In|輸入|Input$|  
  
#### <a name="inspection-functions"></a>檢查函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列檢查函數。  
  
|||||  
|-|-|-|-|  
|IsArray|IsDate|IsEmpty|IsError|  
|IsNull|IsNumeric|IsObject|TypeName|  
|VarType||||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列檢查函數：  
  
-   IsMissing  
  
#### <a name="math-functions"></a>數學函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列數學函數。  
  
|||||  
|-|-|-|-|  
|Abs|Atn|Cos|Exp|  
|Fix|int|Log|Rnd|  
|捨入|Sgn|Sin|Sqr|  
|Tan||||  
  
#### <a name="message-functions"></a>訊息函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不支援下列訊息函數。  
  
|||||  
|-|-|-|-|  
|InputBox|InputBox$|MsgBox||  
  
#### <a name="program-flow-functions"></a>程式流程函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列程式流程函數。  
  
|||||  
|-|-|-|-|  
|Choose|IIf|參數||  
  
#### <a name="sql-aggregate-functions"></a>SQL 彙總函式  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列 SQL 彙總函式。  
  
|||||  
|-|-|-|-|  
|Avg|Count|Max|Min|  
|StDev|StDevP|Sum|Var|  
|VarP||||  
  
#### <a name="text-functions"></a>文字函數  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援下列文字函數。  
  
|||||  
|-|-|-|-|  
|格式|Format$|InStr|InStrRev|  
|LCase|LCase$|Left|Left$|  
|Len|LTrim|LTrim$|Mid|  
|Mid$|取代|Right|Right$|  
|RTrim|Space|Space$|StrComp|  
|StrConv|String|String$|StrReverse|  
|Trim|Trim$|UCase|UCase$|  
  
### <a name="constants"></a>常數  
 Access 不支援運算式中的特殊 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 常數 (例如 `vbTrue`)，所以不需要轉換。 然而，有一個例外：`Null` 關鍵字會轉換成 `System.DbNull.Value`。  
  
### <a name="parameters"></a>參數  
 在匯入程序中，報表設計師會掃描報表中的每一個運算式，找出沒有對應至欄位名稱或控制項的變數。 這些變數會加入報表參數中。  
  
 預存程序參數的資料類型會永遠以字串匯入。 報表匯入之後，您必須手動變更參數，以使用正確的資料類型。  
  
### <a name="object-names"></a>物件名稱  
 Access 允許欄位名稱和控制項名稱相同；[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 則不允許這種情形。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 6.0 允許變數名稱有空格；Visual Basic .NET 則不允許。 匯入程序會將所有這樣的物件名稱，取代為有效的名稱；如果有超過一項物件擁有相同的名稱，匯入程序就會指定唯一的名稱。 匯入程序會掃描每一個運算式，並且會將與重新命名物件對應的變數名稱取代為新的名稱。  
  
## <a name="rectangles-and-containment"></a>矩形和內含項目  
 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表定義中，矩形可以包含其他報表項目。 任何大於報表項目或重疊區域超過百分之 90 的矩形，都會變成報表項目的容器。  
  
## <a name="bitmaps"></a>點陣圖  
 匯入報表時，不論點陣圖的初始格式為何，所有內嵌於報表的點陣圖都會轉換成 .bmp 格式。 例如，如果您的報表包含 .jpg 和 .gif 檔案，隨報表匯入的結果資源都會成為 .bmp 檔案。 點陣圖會以內嵌影像儲存在報表中。 如需有關內嵌影像的資訊，請參閱[影像&#40;報表產生器及 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)。  
  
## <a name="other-considerations"></a>其他考量  
 除了以上項目之外，下列資訊也適用於從 Access 匯入的報表：  
  
-   格式化的條件不會轉換。  
  
-   Access 中的報表屬性的描述欄位不會轉換。  
  
  
