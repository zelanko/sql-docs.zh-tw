---
description: Schema.ini 檔案 (文字檔驅動程式)
title: Schema.ini 檔 (文字檔驅動程式) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b4bbebfa6eb184bf81cba4a9faf5e3200f428de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500221"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 檔案 (文字檔驅動程式)
使用文字驅動程式時，會使用架構資訊檔來決定文字檔的格式。 架構資訊檔一律會命名為 Schema.ini，且一律保留在與文字資料來源相同的目錄中。 架構資訊檔會為 IISAM 提供檔案的一般格式、資料行名稱和資料類型資訊，以及其他數個數據特性的相關資訊。 存取固定長度的資料時，一律需要 Schema.ini 檔。 當您的文字資料表包含 DateTime、Currency 或 Decimal 資料，或您想要更進一步控制資料表中的資料時，您應該使用 Schema.ini 檔案。  
  
> [!NOTE]  
>  Text ISAM 將從登錄取得初始值，而不是從 Schema.ini。 相同的預設檔案格式會套用至所有新的文字資料表。 CREATE TABLE 語句所建立的所有檔案都會繼承這些相同的預設格式值，其設定方式是在 [資料表] 清單中選擇 [**定義文字格式**] 對話方塊中的 [檔案格式值] \<default> **Tables** 。 如果登錄中的值與 Schema.ini 中的值不同，則會以 Schema.ini 的值覆寫登錄中的值。  
  
## <a name="understanding-schemaini-files"></a>瞭解 Schema.ini 檔案  
 Schema.ini 檔案提供文字檔中記錄的架構資訊。 每個 Schema.ini 專案都會指定資料表的五個特性之一：  
  
-   文字檔名稱  
  
-   檔案格式  
  
-   功能變數名稱、寬度和類型  
  
-   字元集  
  
-   特殊資料類型轉換  
  
 下列各節將討論這些特性。  
  
## <a name="specifying-the-file-name"></a>指定檔案名  
 Schema.ini 中的第一個專案一律是以方括弧括住的文字來原始檔案名。 下列範例說明檔案 Sample.txt 的專案：  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>指定檔案格式  
 Schema.ini 中的 **format** 選項會指定文字檔的格式。 文字 IISAM 可以從大多數位符分隔的檔案自動讀取格式。 您可以使用任何單一字元做為檔案中的分隔符號，但雙引號 ( ") 。 Schema.ini 的 **格式** 設定會覆寫 Windows 登錄中的設定（依檔案的檔案）。 下表列出 **Format** 選項的有效值。  
  
|格式規範|資料表格式|Schema.ini 格式語句|  
|----------------------|------------------|---------------------------------|  
|**Tab 分隔**|檔案中的欄位是以定位字元分隔。|格式 = TabDelimited|  
|**CSV 分隔**|檔案中的欄位會以逗號分隔， (逗點分隔值) 。|格式 = CSVDelimited|  
|**自訂分隔**|檔案中的欄位會以您在對話方塊中選擇輸入的任何字元分隔。 除了雙引號以外的所有 ( ") 都是允許的，包括空白。|格式 = 分隔 (*自訂字元*) <br /><br /> -或-<br /><br /> 未指定分隔符號時：<br /><br /> 格式 = 分隔的 ( ) |  
|**固定長度**|檔案中的欄位是固定長度。|格式 = FixedLength|  
  
## <a name="specifying-the-fields"></a>指定欄位  
 您可以用兩種方式在字元分隔的文字檔中指定功能變數名稱：  
  
-   將功能變數名稱包含在資料表的第一個資料列中，並將 **ColNameHeader** 設定為 **True。**  
  
-   依編號指定每個資料行，並指定資料行名稱和資料類型。  
  
 您必須依編號指定每個資料行，並指定固定長度檔案的資料行名稱、資料類型和寬度。  
  
> [!NOTE]  
>  Schema.ini 中的 **ColNameHeader** 設定會覆寫 Windows 登錄中的 **FirstRowHasNames** 設定，依檔案的檔案。  
  
 也可以判斷欄位的資料類型。 使用 **MaxScanRows** 選項，表示在決定資料行類型時，應該掃描的資料列數目。 如果您將 **MaxScanRows** 設定為0，就會掃描整個檔案。 Schema.ini 中的 **MaxScanRows** 設定會覆寫 Windows 登錄中的設定（依檔案的檔案）。  
  
 下列專案表示 Microsoft Jet 應使用資料表第一個資料列中的資料來判斷功能變數名稱，而且應該檢查整個檔案，以判斷所使用的資料類型：  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 下一個專案會使用資料行**編號 (資料**行_n_) 選項來指定資料表中的欄位，這對字元分隔的檔案是選擇性的，而固定長度的檔案則是必要的。 此範例會顯示兩個欄位的 Schema.ini 專案、10個字元的 CustomerNumber 文字欄位和30個字元的 CustomerName 文字欄位：  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 **Col**_n_的語法為：  
  
```  
  
n=ColumnName type [Width] [#]  
```  
  
## <a name="remarks"></a>備註  
 下表描述 **Col**_n_ 專案的每個部分。  
  
|參數|描述|  
|---------------|-----------------|  
|*ColumnName*|資料行的文字名稱。 如果資料行名稱包含內嵌空格，您必須用雙引號括住。|  
|*type*|資料類型如下所示：<br /><br /> **Microsoft Jet 資料類型**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> long<br /><br /> 貨幣<br /><br /> Single<br /><br /> Double<br /><br /> Datetime<br /><br /> Text<br /><br /> 備忘錄<br /><br /> **ODBC 資料類型** Char (與文字相同) <br /><br /> Float (與 Double) 相同<br /><br /> 整數 (與 Short) 相同<br /><br /> LongChar (與備忘錄相同) <br /><br /> 日期 *日期格式*|  
|**寬度**|常值字串值 `Width` 。 指出下列數位會指定資料行的寬度 (選擇性用於字元分隔的檔案;固定長度檔案) 的必要項。|  
|*#*|整數值，如果) 指定 **寬度** ，則指定資料行的寬度 (必要項。|  
  
## <a name="selecting-a-character-set"></a>選取字元集  
 您可以從兩個字元集中選取： ANSI 和 OEM。 Schema.ini 中的 **CharacterSet** 設定會覆寫 Windows 登錄中的設定（依檔案的檔案）。 下列範例顯示將字元集設定為 ANSI 的 Schema.ini 專案：  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>指定資料類型格式和轉換  
 Schema.ini 檔案包含數個選項，可讓您用來指定如何轉換或顯示資料。 下表列出每個選項。  
  
|選項|描述|  
|------------|-----------------|  
|**DateTimeFormat**|可以設定為表示日期和時間的格式字串。 如果匯入/匯出中的所有日期/時間欄位都使用相同的格式來處理，您應該指定此專案。 除了 A.M. 以外的所有 Microsoft Jet 格式 與下午 。 如果沒有格式字串，則會使用 Windows 主控台簡短日期的圖片和時間選項。|  
|**DecimalSymbol**|可以設定為用來分隔整數與數位小數部分的任何單一字元。|  
|**NumberDigits**|表示數位小數部分中的小數位數。|  
|**NumberLeadingZeros**|指定小於1且超過-1 的十進位值是否應包含前置零;這個值可以是 False (沒有前置零) 或 True。|  
|**CurrencySymbol**|指出可用於文字檔中貨幣值的貨幣符號。 範例包括貨幣符號 ($) 和 Dm。|  
|**CurrencyPosFormat**|可以設定為下列任何值：<br /><br /> -沒有分隔 ($1) 的貨幣符號首碼<br />-沒有分隔 ($1) 的貨幣符號尾碼<br />-貨幣符號前置詞，其中包含一個字元分隔 ($1) <br />-以一個字元分隔 ($1) 的貨幣符號尾碼|  
|**CurrencyDigits**|指定貨幣數量之小數部分所使用的位數。|  
|**CurrencyNegFormat**|可以是下列值之一：<br /><br /> - ($1) <br />--$1<br />-$-1<br />-$1-<br />- ($1) <br />--$1<br />-1-$<br />-$1-<br />--$1<br />--$1<br />-$1-<br />-$1-<br />-$-1<br />-1-$<br />- ($1) <br />- ($1) <br /><br /> 此範例顯示貨幣符號，但您應該將它取代為實際程式中的適當 **CurrencySymbol** 值。|  
|**CurrencyThousandSymbol**|表示可以用來將文字檔中的貨幣值分隔為千位的單一字元符號。|  
|**CurrencyDecimalSymbol**|可以設定為用來分隔整個貨幣金額小數部分的任何單一字元。|  
  
> [!NOTE]  
>  如果您省略專案，則會使用 Windows 主控台中的預設值。
