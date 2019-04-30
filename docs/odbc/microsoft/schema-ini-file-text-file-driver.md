---
title: Schema.ini 檔案 （文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 708442d30b571f165f7f9d70f346a958764316d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127902"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 檔案 (文字檔驅動程式)
使用文字驅動程式時，文字檔案的格式取決於使用結構描述資訊檔案。 結構描述資訊檔案是一律名為 Schema.ini，並且永遠保持在相同的目錄，做為文字資料來源中。 此結構描述資訊檔案會提供相關資訊的一般格式的檔案、 資料行名稱和資料型別資訊，以及數個其他資料特性 iisam 開啟。 Schema.ini 檔案總是需要存取固定長度的資料。 當您文字的資料表包含日期時間、 貨幣或十進位資料或任何您想要更充分掌控的資料表中的資料處理的時間，您應該使用 Schema.ini 檔案。  
  
> [!NOTE]  
>  從登錄，而不是從 Schema.ini，文字 ISAM 就會取得初始值。 相同的預設檔案格式適用於所有新的文字資料資料表。 CREATE TABLE 陳述式所建立的所有檔案都繼承這些相同的預設格式值，來選取檔案格式中的值會設定**定義文字格式**對話方塊，其中包含\<預設 >中選擇**資料表**清單。 如果登錄中的值不同於 Schema.ini 中的值，Schema.ini 的值將會覆寫登錄中的值。  
  
## <a name="understanding-schemaini-files"></a>了解 Schema.ini 檔案  
 Schema.ini 檔會提供文字檔案中記錄的結構描述資訊。 每個 Schema.ini 項目會指定其中一個資料表的五種特性：  
  
-   文字檔案名稱  
  
-   檔案格式  
  
-   欄位名稱、 寬度和類型  
  
-   字元集  
  
-   特殊資料類型轉換  
  
 下列各節將討論這些特性。  
  
## <a name="specifying-the-file-name"></a>指定的檔案名稱  
 Schema.ini 第一個項目永遠是以方括弧括住的文字來源檔案的名稱。 下列範例說明 Sample.txt 檔案中的項目：  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>指定的檔案格式  
 **格式**Schema.ini 選項指定的文字檔案格式。 文字 iisam 開啟可讀取格式自動最字元分隔的檔案。 您可以使用任何單一字元做為分隔符號，但雙引號 （"） 檔案中。 **格式**Schema.ini 中的設定會覆寫在 Windows 登錄中，檔案的方式設定。 下表列出的有效值**格式**選項。  
  
|格式規範|資料表格式|Schema.ini Format 陳述式|  
|----------------------|------------------|---------------------------------|  
|**Tab 分隔**|檔案中的欄位是以定位字元分隔。|Format=TabDelimited|  
|**CSV 分隔**|檔案中的欄位是以逗號 （逗號分隔值） 分隔。|格式 = CSVDelimited|  
|**自訂分隔**|您選擇於對話方塊中輸入任何字元分隔檔案中的欄位。 雙引號 （"） 以外的所有允許，包括空白。|格式 = 使用分隔符號 (*自訂字元*)<br /><br /> -或-<br /><br /> 使用指定的任何分隔符號：<br /><br /> Format=Delimited( )|  
|**固定的長度**|檔案中的欄位都是固定的長度。|格式 = FixedLength|  
  
## <a name="specifying-the-fields"></a>指定的欄位  
 您可以指定欄位名稱有兩種字元分隔的文字檔案中：  
  
-   在資料表的第一個資料列中包含的欄位名稱，並設定**ColNameHeader**到 **，則為 True。**  
  
-   指定每個資料行的數目，並指定資料行名稱和資料類型。  
  
 您必須指定每個資料行的數目，並指定資料行名稱、 資料類型和固定長度的檔案的寬度。  
  
> [!NOTE]  
>  **ColNameHeader** Schema.ini 覆寫中設定**FirstRowHasNames**設定在 Windows 登錄中，檔案的方式。  
  
 也可以決定欄位的資料類型。 使用**於 MaxScanRows**選項以指出判斷資料行類型時，所要掃描多少資料列。 如果您設定**於 MaxScanRows**為 0，會掃描整個檔案。 **於 MaxScanRows** Schema.ini 中的設定會覆寫在 Windows 登錄中，檔案的方式設定。  
  
 下列項目表示 Microsoft Jet 應該使用資料表的第一個資料列中的資料，來判斷欄位名稱，而且應該檢查以判斷資料的整個檔案所使用的類型：  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 下一個項目會指定資料表中的欄位使用的資料行編號 (**Col**_n_) 選項，這是字元分隔檔案的選擇性及必要的固定長度的檔案。 此範例示範兩個欄位、 10 個字元 CustomerNumber 文字欄位和 30 個字元 CustomerName 文字欄位的 Schema.ini 項目：  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 語法**Col**_n_是：  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>備註  
 下表描述的每個部分**Col**_n_項目。  
  
|參數|描述|  
|---------------|-----------------|  
|*ColumnName*|文字資料行的名稱。 如果資料行名稱包含內嵌的空格，您必須將它括在雙引號中。|  
|*type*|資料類型如下所示：<br /><br /> **Microsoft Jet 資料類型**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> 長整數<br /><br /> CURRENCY<br /><br /> Single<br /><br /> Double<br /><br /> Datetime<br /><br /> Text<br /><br /> 備忘錄<br /><br /> **ODBC 資料類型**Char （相同的文字）<br /><br /> Float （與 Double 相同）<br /><br /> 整數 （Short 與相同）<br /><br /> LongChar （如同備忘）<br /><br /> 日期*日期格式*|  
|**寬度**|常值字串值`Width`。 指出下列數字指定的資料行的寬度 （選擇性的字元分隔的檔案; 需要固定長度的檔案）。|  
|*#*|指定資料行寬度的整數值 (需要**寬度**指定)。|  
  
## <a name="selecting-a-character-set"></a>選取的字元集  
 您可以選取從兩個字元集：ANSI 和 OEM。 **CharacterSet** Schema.ini 中的設定會覆寫在 Windows 登錄中，檔案的方式設定。 下列範例顯示設定為 ANSI 字元集的 Schema.ini 項目：  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>指定資料型別格式和轉換  
 Schema.ini 檔案包含數個選項可用來指定如何轉換或顯示資料。 下表列出每個選項。  
  
|選項|描述|  
|------------|-----------------|  
|**DateTimeFormat**|可以設定為格式字串，表示日期和時間。 如果在匯入/匯出的所有日期/時間欄位會都處理相同的格式，您應該指定這個項目。 所有的 Microsoft Jet 格式，除了 A.M. 和下午 支援。 如果沒有任何格式字串，則會使用 Windows 控制台中的簡短日期圖片和時間選項。|  
|**DecimalSymbol**|可以設定為用來分隔的整數，從數字的小數部分的任何單一字元。|  
|**NumberDigits**|表示數字的小數部分的十進位數字的數目。|  
|**NumberLeadingZeros**|指定小於 1 及以上-1 的十進位值是否應該包含前置的零;這個值可以是任一個為 False （沒有前置的零） 或 True。|  
|**CurrencySymbol**|表示可以用於文字檔案中的貨幣值的貨幣符號。 範例包括貨幣符號 （$） 和 Dm。|  
|**CurrencyPosFormat**|可以設定為下列值之一：<br /><br /> -貨幣符號前置詞，而且沒有區隔 ($1)<br />-貨幣符號後的置詞與沒有區隔 (1$)<br />-貨幣符號前置詞，和一個字元分隔 ($ 1)<br />-貨幣符號後的置詞與一個字元分隔 (1 $)|  
|**CurrencyDigits**|指定用於貨幣金額的小數部分的位數。|  
|**CurrencyNegFormat**|可為下列其中一個值：<br /><br /> -   ($1)<br />-   -$1<br />-   $-1<br />-   $1-<br />-   (1$)<br />-   -1$<br />-   1-$<br />-   1$-<br />-   -1 $<br />-   -$ 1<br />-   1 $-<br />-   $ 1-<br />-   $ -1<br />-   1- $<br />-   ($ 1)<br />-   (1 $)<br /><br /> 此範例顯示貨幣符號，但您應該更換適當**CurrencySymbol**實際的程式中的值。|  
|**CurrencyThousandSymbol**|表示可以用來分隔文字檔案中的貨幣值，以千為單位的單一字元符號。|  
|**CurrencyDecimalSymbol**|可以設定為用來分隔貨幣金額的小數部分與整體的任何單一字元。|  
  
> [!NOTE]  
>  如果您省略項目時，會使用 Windows 控制台中的預設值。
