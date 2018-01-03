---
title: "Schema.ini 檔 （文字檔案驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0b71b742ff9c0833bd36deb256dda5169f2a51c7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 檔 （文字檔案驅動程式）
使用文字驅動程式時，文字檔案的格式取決於使用結構描述資訊檔案。 是一律名為 Schema.ini 的結構描述資訊的檔案，並永遠保持在相同的目錄做為文字資料來源中。 結構描述資訊檔案提供 IISAM 有關的一般格式的檔案、 資料行名稱和資料型別資訊，以及數個其他資料特性的資訊。 Schema.ini 檔所需存取固定長度的資料。 當文字資料表包含的日期時間、 貨幣或十進位資料或每次您要更充分掌控資料表中資料的處理時，您應該使用 Schema.ini 檔案。  
  
> [!NOTE]  
>  從登錄，而不是從 Schema.ini 文字 ISAM 就會取得初始值。 相同的預設檔案格式適用於所有新的文字資料表格。 CREATE TABLE 陳述式所建立的所有檔案會都繼承這些相同的預設格式值，而這藉由選取檔案格式中的值設定**定義文字格式**對話方塊\<預設 >中選擇**資料表**清單。 如果在登錄中的值與 Schema.ini 中的值不同，Schema.ini 的值將會覆寫登錄中的值。  
  
## <a name="understanding-schemaini-files"></a>了解 Schema.ini 檔案  
 Schema.ini 檔案提供文字檔案中記錄的結構描述資訊。 每個 Schema.ini 項目會指定其中一個資料表的五種特性：  
  
-   文字檔案名稱  
  
-   檔案格式  
  
-   欄位名稱、 寬度和類型  
  
-   字元集  
  
-   特殊資料類型轉換  
  
 下列章節會討論這些特性。  
  
## <a name="specifying-the-file-name"></a>指定的檔案名稱  
 Schema.ini 中的第一個項目永遠是以方括弧括住的文字來源檔的名稱。 下列範例將說明檔案 Sample.txt 的項目：  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>指定的檔案格式  
 **格式**中 Schema.ini 選項指定的文字檔案格式。 文字 IISAM 可讀取的格式自動最字元分隔的檔案。 您可以使用任何單一字元做為分隔符號，但雙引號 （"） 檔案中。 **格式**Schema.ini 中的設定會覆寫 Windows 登錄、 檔案的檔案中的設定。 下表列出的有效值**格式**選項。  
  
|格式規範|資料表格式|Schema.ini Format 陳述式|  
|----------------------|------------------|---------------------------------|  
|**Tab 字元分隔**|Tab 鍵分隔檔案中的欄位。|格式 = TabDelimited|  
|**CSV 分隔**|使用逗點 （以逗號分隔值） 分隔檔案中的欄位。|格式 = CSVDelimited|  
|**自訂分隔符號**|檔案中的欄位是以您選擇在對話方塊中輸入任何字元分隔。 雙引號 （"） 以外的所有允許，包括空白。|格式 = 分隔符號 (*自訂字元*)<br /><br /> -或-<br /><br /> 使用指定的任何分隔符號：<br /><br /> 格式 = 分隔 （）|  
|**固定的長度**|檔案中的欄位都是固定的長度。|格式 = FixedLength|  
  
## <a name="specifying-the-fields"></a>指定的欄位  
 您可以指定欄位名稱中有兩種字元分隔的文字檔案：  
  
-   在資料表的第一個資料列中包含的欄位名稱，並設定**ColNameHeader**至**，則為 True。**  
  
-   指定每個資料行的數目，並指定資料行名稱和資料類型。  
  
 您必須指定每個資料行的數目，並指定資料行名稱、 資料類型和固定長度的檔案的寬度。  
  
> [!NOTE]  
>  **ColNameHeader** Schema.ini 覆寫中設定**FirstRowHasNames**設定在 Windows 登錄中，檔案的檔案。  
  
 也可以決定欄位的資料類型。 使用**於 MaxScanRows**選項來指示應該掃描多少資料列，判斷資料行型別時。 如果您設定**於 MaxScanRows**為 0，會掃描整個檔案。 **於 MaxScanRows** Schema.ini 中的設定會覆寫 Windows 登錄、 檔案的檔案中的設定。  
  
 下列項目表示，Microsoft Jet 應該使用資料表的第一個資料列中的資料，以決定欄位的名稱，而且應該會檢查整個檔案，以判斷資料類型使用：  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 下一個項目會指定資料表中的欄位使用的資料行編號 (**Col***n*) 字元分隔檔案的選擇性且固定長度的檔案需要的選項。 此範例示範兩個欄位、 10 個字元 CustomerNumber 文字欄位和 30 個字元 CustomerName 文字欄位的 Schema.ini 項目：  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 語法**Col**  *n* 是：  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>備註  
 下表說明每一部分**Col**  *n* 項目。  
  
|參數|描述|  
|---------------|-----------------|  
|*ColumnName*|文字資料行的名稱。 如果資料行名稱包含內嵌的空格，您必須將它括在雙引號中。|  
|*type*|資料類型如下所示：<br /><br /> **Microsoft Jet 資料類型**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> 長整數<br /><br /> CURRENCY<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> 文字<br /><br /> 備忘錄<br /><br /> **ODBC 資料類型**Char （如同文字）<br /><br /> Float （與 Double 相同）<br /><br /> 整數 （如同 Short）<br /><br /> LongChar （如同備忘）<br /><br /> 日期*日期格式*|  
|**寬度**|常值字串值`Width`。 表示下列的數字指定的資料行寬度 （可選擇性地用於字元分隔的檔案; 固定長度的檔案需要）。|  
|*#*|指定資料行寬度的整數值 (若**寬度**指定)。|  
  
## <a name="selecting-a-character-set"></a>選取的字元集  
 您可以選取從兩個字元集： ANSI 和 OEM。 **CharacterSet** Schema.ini 中的設定會覆寫 Windows 登錄、 檔案的檔案中的設定。 下列範例示範設定為 ANSI 字元集的 Schema.ini 項目：  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>指定資料類型的格式和轉換  
 Schema.ini 檔會包含數個選項可讓您指定如何轉換或顯示資料。 下表列出每個選項。  
  
|選項|描述|  
|------------|-----------------|  
|**DateTimeFormat**|可以將格式字串，表示日期和時間。 如果在匯入/匯出的所有日期/時間欄位會都處理相同的格式，您應該指定這個項目。 上午以外的所有 Microsoft Jet 格式 到下午 支援。 如果沒有任何格式字串，則會使用 Windows 控制台中的簡短日期圖片和時間選項。|  
|**DecimalSymbol**|可以設定用來分隔整數從一個數字的小數部分的任何單一字元。|  
|**NumberDigits**|表示數字的小數部分的十進位數字的數目。|  
|**NumberLeadingZeros**|指定的十進位值小於 1，多個 – 1 表示是否應該包含前置的零。這個值可以是 （沒有前置的零） 是 False 或 True。|  
|**CurrencySymbol**|表示可以使用文字檔案中的貨幣值的貨幣符號。 範例包括貨幣符號 （$） 和資料採礦。|  
|**CurrencyPosFormat**|可以設定為下列值之一：<br /><br /> 使用無隔離 ($1) 的貨幣符號前置詞<br />使用無隔離的貨幣符號尾碼 (1$)<br />貨幣符號前置詞與一個字元分隔 ($ 1)<br />貨幣符號後置字元的一個字元分隔 (1 $)|  
|**CurrencyDigits**|指定用於貨幣金額的小數部分的位數。|  
|**CurrencyNegFormat**|可以是下列其中一個值：<br /><br /> -   ($1)<br />-   –$1<br />-   $–1<br />-   $1–<br />-   (1$)<br />-   –1$<br />-   1–$<br />-   1$–<br />-   –1 $<br />-   –$ 1<br />-   1 $–<br />-   $ 1–<br />-   $ –1<br />-   1– $<br />-   ($ 1)<br />-   (1 $)<br /><br /> 此範例顯示貨幣符號，但您應該更換適當**CurrencySymbol**實際的程式中的值。|  
|**CurrencyThousandSymbol**|表示可以用來分隔文字檔案中的貨幣值，以千為單位的單一字元符號。|  
|**CurrencyDecimalSymbol**|可以設定用來分隔從貨幣金額的小數部分與整體的任何單一字元。|  
  
> [!NOTE]  
>  如果您省略某個項目時，會使用控制台中的 Windows 中的預設值。
