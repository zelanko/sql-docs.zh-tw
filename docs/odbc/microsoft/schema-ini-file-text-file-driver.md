---
title: 架構 .ini 檔案（文字檔驅動程式） |Microsoft Docs
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
ms.openlocfilehash: dd95329c91c69af38b1ffc7951191498fcc40479
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987943"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 檔案 (文字檔驅動程式)
使用文字驅動程式時，會使用架構資訊檔案來決定文字檔的格式。 架構資訊檔案一律命名為 schema.ini，而且一律會保留在與文字資料來源相同的目錄中。 架構資訊檔案會提供 IISAM，其中包含檔案的一般格式資訊、資料行名稱和資料類型資訊，以及其他數個數據特性。 存取固定長度的資料時，一律需要使用 schema.ini 檔案。 當您的文字資料表包含日期時間、貨幣或十進位資料，或您想要更充分掌控資料表中的資料處理時，您應該使用 schema.ini 檔案。  
  
> [!NOTE]  
>  [ISAM] 文字將會從登錄取得初始值，而不是從架構 .ini。 相同的預設檔案格式會套用到所有新的文字資料表。 CREATE TABLE 語句所建立的所有檔案都會繼承那些相同的預設格式值，其設定方式是在 [**定義文字格式**] 對話方塊中，選取 [ \<**資料表**] 清單中所選擇的預設> 的 [檔案格式值]。 如果登錄中的值與 schema.ini 中的值不同，則登錄中的值將會由 schema.ini 中的值覆寫。  
  
## <a name="understanding-schemaini-files"></a>瞭解架構 .ini 檔案  
 架構 .ini 檔案提供文字檔中記錄的相關架構資訊。 每個 schema.ini 專案都會指定資料表的五個特性之一：  
  
-   文字檔名稱  
  
-   檔案格式  
  
-   功能變數名稱、寬度和類型  
  
-   字元集  
  
-   特殊資料類型轉換  
  
 下列各節將討論這些特性。  
  
## <a name="specifying-the-file-name"></a>指定檔案名  
 Schema.ini 中的第一個專案一律是以方括弧括住的文字來原始檔案名。 下列範例說明檔案範例 .txt 的專案：  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>指定檔案格式  
 Schema.ini 中的**format**選項會指定文字檔的格式。 文字 IISAM 可以從大部分以字元分隔的檔案自動讀取格式。 您可以使用任何單一字元做為檔案中的分隔符號，但雙引號（"）除外。 Schema.ini 中的**格式**設定會覆寫 Windows 登錄中的設定（依檔案）。 下表列出**Format**選項的有效值。  
  
|格式規範|資料表格式|Schema.ini 格式語句|  
|----------------------|------------------|---------------------------------|  
|**Tab 鍵分隔**|檔案中的欄位會以定位字元分隔。|格式 = TabDelimited|  
|**CSV 分隔**|檔案中的欄位是以逗號分隔（以逗號分隔的值）。|格式 = CSVDelimited|  
|**自訂分隔**|檔案中的欄位會以您選擇輸入至對話方塊的任何字元來分隔。 除了雙引號（"）以外，所有的都是允許的，包括空白。|格式 = 分隔（*自訂字元*）<br /><br /> -或-<br /><br /> 未指定分隔符號：<br /><br /> Format = 分隔（）|  
|**固定長度**|檔案中的欄位是固定長度。|格式 = FixedLength|  
  
## <a name="specifying-the-fields"></a>指定欄位  
 您可以透過兩種方式，在以字元分隔的文字檔中指定功能變數名稱：  
  
-   在資料表的第一個資料列中包含功能變數名稱，並將**ColNameHeader**設定為**True。**  
  
-   依數位指定每個資料行，並指定資料行名稱和資料類型。  
  
 您必須依數位指定每個資料行，並指定固定長度檔案的資料行名稱、資料類型和寬度。  
  
> [!NOTE]  
>  Schema.ini 中的**ColNameHeader**設定會覆寫 Windows 登錄中的**FirstRowHasNames**設定，依檔案的檔案。  
  
 您也可以決定欄位的資料類型。 使用**MaxScanRows**選項，以指出在判斷資料行類型時，應該掃描多少資料列。 如果您將**MaxScanRows**設定為0，就會掃描整個檔案。 Schema.ini 中的**MaxScanRows**設定會覆寫 Windows 登錄中的設定（依檔案）。  
  
 下列專案表示 Microsoft Jet 應該使用資料表第一列中的資料來判斷功能變數名稱，而且應該檢查整個檔案以判斷所使用的資料類型：  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 下一個專案會使用 [資料行編號（第_n_**欄**）] 選項來指定資料表中的欄位，這對字元分隔檔案而言是選擇性的，而固定長度檔案則是必要的。 此範例會顯示兩個欄位的 schema.ini 專案，一個是10個字元的 CustomerNumber 文字欄位，一個是30個字元的 CustomerName 文字欄位：  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 **Col**_n_的語法為：  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>備註  
 下表描述的是**Col**_n_專案的每個部分。  
  
|參數|描述|  
|---------------|-----------------|  
|*ColumnName*|資料行的文字名稱。 如果資料行名稱包含內嵌的空格，您必須將它括在雙引號中。|  
|*type*|資料類型如下所示：<br /><br /> **Microsoft Jet 資料類型**<br /><br /> bit<br /><br /> Byte<br /><br /> 簡短<br /><br /> long<br /><br /> 貨幣<br /><br /> Single<br /><br /> DOUBLE<br /><br /> Datetime<br /><br /> Text<br /><br /> 備忘錄<br /><br /> **ODBC 資料類型**Char （與文字相同）<br /><br /> Float （與 Double 相同）<br /><br /> 整數（與 Short 相同）<br /><br /> LongChar （與備忘）<br /><br /> 日期*日期格式*|  
|**寬度**|常值字串值`Width`。 指出下列數位會指定資料行的寬度（針對以字元分隔的檔案而言為選擇性，固定長度檔案則為必要項）。|  
|*#*|指定資料行寬度的整數值（如果已指定**width** ，則為必要）。|  
  
## <a name="selecting-a-character-set"></a>選取字元集  
 您可以從兩個字元集中進行選取： ANSI 和 OEM。 Schema.ini 中的**CharacterSet**設定會覆寫 Windows 登錄中的設定（依檔案）。 下列範例顯示將字元集設定為 ANSI 的 schema.ini 專案：  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>指定資料類型格式和轉換  
 Schema.ini 檔案包含數個選項，您可以用來指定轉換或顯示資料的方式。 下表列出每個選項。  
  
|選項|描述|  
|------------|-----------------|  
|**DateTimeFormat**|可以設定為表示日期和時間的格式字串。 如果匯入/匯出中所有的日期/時間欄位都是以相同的格式處理，您就應該指定這個專案。 所有 Microsoft Jet 格式，不包括 A.M。 與下午 。 如果沒有格式字串，則會使用 Windows [控制台] [簡短日期] 圖片和 [時間] 選項。|  
|**DecimalSymbol**|可以設定為用來分隔整數與數位小數部分的任何單一字元。|  
|**NumberDigits**|表示數位小數部分中的小數位數。|  
|**NumberLeadingZeros**|指定小於1且大於-1 的十進位值是否應包含前置零;這個值可以是 False （沒有前置零）或 True。|  
|**CurrencySymbol**|表示可用於文字檔中貨幣值的貨幣符號。 範例包括貨幣符號（$）和 Dm。|  
|**CurrencyPosFormat**|可以設定為下列任何值：<br /><br /> -沒有分隔的貨幣符號前置詞（$1）<br />-沒有分隔的貨幣符號尾碼（$1）<br />-貨幣符號前置詞加上一個字元分隔（$1）<br />-包含一個字元分隔的貨幣符號尾碼（$1）|  
|**CurrencyDigits**|指定貨幣金額小數部分所使用的位數。|  
|**CurrencyNegFormat**|可以是下列其中一個值：<br /><br /> -（$1）<br />--$1<br />-$-1<br />-$1-<br />-（$1）<br />--$1<br />-1-$<br />-$1-<br />--$1<br />--$1<br />-$1-<br />-$1-<br />-$-1<br />-1-$<br />-（$1）<br />-（$1）<br /><br /> 這個範例會顯示貨幣符號，但您應該以實際程式中的適當**CurrencySymbol**值來取代它。|  
|**CurrencyThousandSymbol**|表示可以用來將文字檔中的貨幣值分隔為千位的單一字元符號。|  
|**CurrencyDecimalSymbol**|可以設定為用來分隔整個貨幣金額小數部分的任何單一字元。|  
  
> [!NOTE]  
>  如果您省略專案，則會使用 Windows [控制台] 中的預設值。
