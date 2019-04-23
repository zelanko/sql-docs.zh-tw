---
title: 運算式中的資料類型 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 94fdf921-270c-4c12-87b3-46b1cc98fae5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5b0af16c21cb9fdf2c8ab41a931f955b46c29352
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59956104"
---
# <a name="data-types-in-expressions-report-builder-and-ssrs"></a>運算式中的資料類型 (報表產生器及 SSRS)
  資料類型代表不同種類的資料，以便讓系統能夠有效率地儲存和處理資料。 一般資料類型包括文字 (也稱為字串)、含與不含小數位數的數字、日期和時間，以及影像。 報表中的值必須是報表定義語言 (RDL) 資料類型。 當您在報表中顯示值時，可以根據您的喜好設定來格式化值。 例如，代表貨幣的欄位會當做浮點數儲存在報表定義中，但是可能會根據您選擇的格式屬性，以各種格式顯示此欄位。  
  
 如需顯示格式的詳細資訊，請參閱 [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-language-rdl-data-types-and-common-language-runtime-clr-data-types"></a>報表定義語言 (RDL) 資料類型與 Common Language Runtime (CLR) 資料類型  
 RDL 檔案中所指定的值必須是 RDL 資料類型。 當報表進行編譯和處理時，RDL 資料類型會轉換成 CLR 資料類型。 下表會顯示標示為預設值的轉換：  
  
|RDL 類型|CLR 類型|  
|--------------|---------------|  
|String|預設：String<br /><br /> Chart、GUID、Timespan|  
|布林|預設：布林|  
|Integer|預設：Int64<br /><br /> Int16、Int32、Uint16、Uint64、Byte、Sbyte|  
|Datetime|預設：Datetime<br /><br /> DateTimeOffset|  
|float|預設：Double<br /><br /> Single、Decimal|  
|二進位|預設：Byte[]|  
|變數|除了 Byte[] 之外，以上任何一種|  
|VariantArray|變數的陣列|  
|可序列化|標示為 Serializable 或實作 ISerializable 的變數或類型。|  
  
## <a name="understanding-data-types-and-writing-expressions"></a>了解資料類型與撰寫運算式  
 當您撰寫運算式來比較或結合值 (例如，定義群組或篩選運算式，或者計算彙總) 時，了解資料類型便相當重要。 比較和計算作業只能在相同資料類型的項目之間進行。 如果資料類型不相符，您就必須使用運算式來明確轉換報表項目中的資料類型。  
  
 下列清單將描述您必須將資料轉換成不同資料類型的情況：  
  
-   比較某種資料類型的報表參數值與不同資料類型的資料集欄位。  
  
-   撰寫比較不同資料類型之值的篩選運算式。  
  
-   撰寫結合不同資料類型之欄位的排序運算式。  
  
-   撰寫結合不同資料類型之欄位的群組運算式。  
  
-   將資料來源中擷取的值，從某種資料類型轉換成不同的資料類型。  
  
## <a name="determining-the-data-type-of-report-data"></a>判斷報表資料的資料類型  
 若要判斷報表項目的資料類型，您可以撰寫傳回其資料類型的運算式。 例如，若要顯示欄位 `MyField`的資料類型，請將下列運算式加入至資料表的資料格： `=Fields!MyField.Value.GetType().ToString()`。 結果會顯示用來代表 `MyField` 的 CLR 資料類型，例如 `System.String` 或 `System.DateTime`。  
  
## <a name="converting-dataset-fields-to-a-different-data-type"></a>將資料集欄位轉換成不同的資料類型  
 您也可以先轉換資料集欄位，然後再將它們用於報表中。 下列清單將描述您可以轉換現有資料集欄位的方式：  
  
-   修改資料集查詢，以便加入含有已轉換資料的新查詢欄位。 若為關聯式或多維度資料來源，這項作業會使用資料來源資源來執行轉換。  
  
-   透過撰寫將某個結果集資料行中所有資料轉換成含有不同資料類型之新資料行的運算式，根據現有的報表資料集欄位建立導出欄位。 例如，下列運算式會將欄位 Year 從整數值轉換成字串值： `=CStr(Fields!Year.Value)`。 如需詳細資訊，請參閱[加入、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。  
  
-   檢查您所使用的資料處理延伸模組是否包含擷取預先格式化資料的中繼資料。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX 查詢會針對處理 Cube 時已經格式化的 Cube 值包含 FORMATTED_VALUE 擴充屬性。 如需詳細資訊，請參閱 [Analysis Services 資料庫的擴充欄位屬性 &#40;SSRS&#41;](../report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)。  
  
## <a name="understanding-parameter-data-types"></a>了解參數資料類型  
 報表參數必須是下列五種資料類型其中之一：Boolean、DateTime、Integer、Float 或 Text (也稱為 String)。 當資料集查詢包含查詢參數時，系統就會自動建立報表參數並將它們連結至查詢參數。 報表參數的預設資料類型為 String。 若要變更報表參數的預設資料類型，請在 [報表參數屬性] 對話方塊的 [一般] 頁面上，從 [資料類型] 下拉式清單中選取正確的值。  
  
> [!NOTE]  
>  屬於 DateTime 資料類型的報表參數不支援毫秒。 雖然您可以根據包含毫秒的值建立參數，但是無法從包含毫秒之日期或時間值的可用值下拉式清單中選取值。  
  
## <a name="writing-expressions-that-convert-data-types-or-extract-parts-of-data"></a>撰寫轉換資料類型或擷取部分資料的運算式  
 當您使用串連運算子 (&) 來結合文字和資料集欄位時，Common Language Runtime (CLR) 通常會提供預設格式。 當您必須將資料集欄位或參數轉換成特定資料類型時，就必須使用 CLR 方法或 Visual Basic 執行階段程式庫函數來轉換資料。  
  
 下表將顯示轉換資料類型的範例。  
  
|轉換的類型|範例|  
|------------------------|-------------|  
|DateTime 轉換成 String|`=CStr(Fields!Date.Value)`|  
|String 轉換成 DateTime|`=DateTime.Parse(Fields!DateTimeinStringFormat.Value)`|  
|String 轉換成 DateTimeOffset|`=DateTimeOffset.Parse(Fields!DateTimeOffsetinStringFormat.Value)`|  
|擷取年份|`=Year(Fields!TimeinStringFormat.Value)`<br /><br /> `-- or --`<br /><br /> `=Year(Fields!TimeinDateTimeFormat.Value)`|  
|Boolean 轉換成 Integer|`=CInt(Parameters!BooleanField.Value)`<br /><br /> -1 為 True 而 0 為 False。|  
|Boolean 轉換成 Integer|`=System.Convert.ToInt32(Fields!BooleanFormat.Value)`<br /><br /> 1 為 True 而 0 為 False。|  
|只有 DateTimeOffset 值的 DateTime 部分|`=Fields!MyDatetimeOffset.Value.DateTime`|  
|只有 DateTimeOffset 值的 Offset 部分|`=Fields!MyDatetimeOffset.Value.Offset`|  
  
 您也可以使用 Format 函數來控制值的顯示格式。 如需詳細資訊，請參閱 [函式 (Visual Basic)](https://go.microsoft.com/fwlink/?linkid=111483)。  
  
## <a name="advanced-examples"></a>進階範例  
 當您連接至某個資料來源，但是所使用的資料提供者並未提供該資料來源之所有資料類型的轉換支援時，不支援之資料來源類型的預設資料類型就是 String。 下列範例會提供當做字串傳回之特定資料類型的解決方案。  
  
### <a name="concatenating-a-string-and-a-clr-datetimeoffset-data-type"></a>串連 String 和 CLR DateTimeOffset 資料類型  
 CLR 會針對大部分資料類型提供預設轉換，讓您能夠使用 & 運算子，將不同資料類型的值串連成單一字串。 例如，下列運算式會串連文字 "The date and time are: " 與資料集欄位 StartDate (它是 <xref:System.DateTime> 值)： `="The date and time are: " & Fields!StartDate.Value`。  
  
 若為某些資料類型，您可能就必須加入 ToString 函數。 例如，下列運算式會使用 CLR 資料類型 <xref:System.DateTimeOffset>來顯示相同的範例，其中包含日期、時間和相對於 UTC 時區的時區時差： `="The time is: " & Fields!StartDate.Value.ToString()`。  
  
### <a name="converting-a-string-data-type-to-a-clr-datetime-data-type"></a>將 String 資料類型轉換成 CLR DateTime 資料類型  
 如果資料處理延伸模組不支援針對資料來源所定義的所有資料類型，系統可能會將資料擷取成文字。 例如，`datetimeoffset(7)` 資料類型值可能會擷取成 String 資料類型。 在澳大利亞的伯斯省，代表 2008 年 7 月 1 日上午 6:05:07.9999999 的字串值 會類似下列內容：  
  
 `2008-07-01 06:05:07.9999999 +08:00`  
  
 這個範例會顯示日期 (2008 年 7 月 1 日)、接著 7 位數精確度的時間 (上午 6:05:07.9999999)，然後接著以小時和分鐘為單位的 UTC 時區時差 (加上 8 小時，0 分)。 在下列範例中，這個值已經放置於稱為 `MyDateTime.Value` 的 `String` 欄位中。  
  
 您可以使用下列其中一種策略，將這項資料轉換成一個或多個 CLR 值：  
  
-   在文字方塊中，使用運算式來擷取部分字串。 例如：  
  
    -   下列運算式只會擷取 UTC 時區時差的小時部分，並將它轉換成分鐘： `=CInt(Fields!MyDateTime.Value.Substring(Fields!MyDateTime.Value.Length-5,2)) * 60`  
  
         結果為 `480`。  
  
    -   下列運算式會將字串轉換成日期和時間值： `=DateTime.Parse(Fields!MyDateTime.Value)`  
  
         如果 `MyDateTime.Value` 字串具有 UTC 時差， `DateTime.Parse` 函數會先針對 UTC 時差調整 (上午 7 點 - [`+08:00`] 調整成前一晚 11 點的 UTC 時間)。 然後， `DateTime.Parse` 函數會套用本機報表伺服器 UTC 時差，並在必要時，再次針對日光節約時間調整時間。 例如，在華盛頓州的雷德蒙市，針對日光節約時間調整的本地時間時差是 `[-07:00]`，或下午 11 點之前的 7 個小時。 結果就是下列`DateTime`值：`2007-07-06 04:07:07 PM` (2007 年 7 月 6 日下午 4:07)。  
  
 如需有關將字串轉換成`DateTime`資料類型，請參閱[剖析的日期和時間字串](https://go.microsoft.com/fwlink/?LinkId=89703)，[格式的日期和時間的特定文化特性](https://go.microsoft.com/fwlink/?LinkId=89704)，和[選擇在 DateTime、 DateTimeOffset 和 TimeZoneInfo 之間](https://go.microsoft.com/fwlink/?linkid=110652)MSDN 上。  
  
-   將新的導出欄位加入至報表資料集，以便使用運算式來擷取部分字串。 如需詳細資訊，請參閱[加入、編輯、重新整理報表資料窗格中的欄位 &#40;報表產生器及 SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。  
  
-   將報表資料集查詢變更成使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數來獨立擷取日期與時間值，以便建立個別的資料行。 下列範例將示範如何使用函數 `DatePart` 來加入代表年份的資料行，以及轉換成分鐘之 UTC 時區的資料行：  
  
     `SELECT`  
  
     `MyDateTime,`  
  
     `DATEPART(year, MyDateTime) AS Year,`  
  
     `DATEPART(tz, MyDateTime) AS OffsetinMinutes`  
  
     `FROM MyDates`  
  
     結果集含有三個資料行。 第一個資料行是日期和時間、第二個資料行是年份，而第三個資料行是 UTC 時差 (以分鐘為單位)。 以下資料列是範例資料示範：  
  
     `2008-07-01 06:05:07             2008                   480`  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫資料類型的詳細資訊，請參閱 [SQL Server 線上叢書](https://go.microsoft.com/fwlink/?linkid=120955)中的[資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) 及[日期和時間資料類型與函數 &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料類型的詳細資訊，請參閱《 [SQL Server 線上叢書](../../analysis-services/multidimensional-models/olap-physical/data-types-in-analysis-services.md) 》中的 [SQL Server Books Onl》中的e](https://go.microsoft.com/fwlink/?linkid=120955)。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)  
  
  
