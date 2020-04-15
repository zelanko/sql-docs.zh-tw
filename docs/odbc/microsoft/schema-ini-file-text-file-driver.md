---
title: 架構.ini 檔案(文字檔案驅動程式) |微軟文件
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
ms.openlocfilehash: 365351724f27205e7d460c757f1268d042cefc76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305509"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 檔案 (文字檔驅動程式)
使用文字驅動程式時,將使用架構資訊檔確定文本檔的格式。 架構資訊文件始終名為 Schema.ini,並且始終與文本數據源保存在同一目錄中。 架構資訊檔向 IISAM 提供有關檔一般格式、列名和數據類型資訊以及其他幾個資料特徵的資訊。 訪問固定長度數據始終需要架構.ini 檔。 當文字表包含 DateTime、貨幣或十進位資料時,或者您希望對表中資料的處理進行更多控制的任何時間,應使用 Schema.ini 檔。  
  
> [!NOTE]  
>  文本 ISAM 將從註冊表獲取初始值,而不是從 Schema.ini 獲取初始值。 相同的預設檔案格式適用於所有新的文本資料表。 CREATE TABLE 敘述建立的所有檔案都繼承相同的預設格式值,這些值是透過在 **'定義文字格式'** 對話框\<中選擇檔案格式值(預設>在 **"表清單**中選擇)來設置的。 如果註冊表中的值與 Schema.ini 中的值不同,則註冊表中的值將被架構.ini 中的值覆蓋。  
  
## <a name="understanding-schemaini-files"></a>瞭解架構.ini 檔案  
 Schema.ini 檔案提供有關文本檔中記錄的架構資訊。 每個架構.ini 條目指定表的五個特徵之一:  
  
-   文字檔名  
  
-   檔案格式  
  
-   欄位名稱、寬度和類型  
  
-   字元集  
  
-   特殊資料型別轉換  
  
 以下各節討論這些特徵。  
  
## <a name="specifying-the-file-name"></a>指定檔案名稱  
 Schema.ini 中的第一個條目始終是包含在方括弧中的文本源檔的名稱。 下面的範例說明了檔案 Sample.txt 的項目:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>指定檔案格式  
 Schema.ini 中的**格式'** 選項指定文字檔的格式。 文字 IISAM 可以從大多數字元分隔檔中自動讀取格式。 除了雙引號 () 之外,可以使用任何單個字元作為檔中的分隔符。 架構中的 **「格式」** 設定將覆蓋 Windows 註冊表中的設定,按檔進行。 下表列出了 **「格式」** 選項的有效值。  
  
|格式規範|表格式|架構.ini 格式語句|  
|----------------------|------------------|---------------------------------|  
|**選項卡分隔**|檔案中的欄位由選項卡分隔。|格式=標籤限制|  
|**CSV 限制**|檔案中的欄位按逗號(逗號分隔值)分隔。|格式_CSVDe有限|  
|**自訂分隔**|檔案中的欄位由您選擇輸入到對話框中的任何字元分隔。 除雙引號 (") 外,所有內容均允許,包括空白。|格式=分隔(*自訂字元*)<br /><br /> -或-<br /><br /> 沒有指定分隔符:<br /><br /> 格式=限制)|  
|**固定長度**|檔中的欄位長度固定。|格式 =固定長度|  
  
## <a name="specifying-the-fields"></a>指定欄位  
 您可以透過兩種方式在字元分隔文字檔中指定欄位名稱:  
  
-   在表的第一行中包括欄位名稱,並將**ColNameHeader**設定為**True。**  
  
-   依數位指定每列並指定列名稱和數據類型。  
  
 您必須按數位指定每列,並為固定長度的檔指定列名稱、數據類型和寬度。  
  
> [!NOTE]  
>  架構中的**ColNameHeader**設定將覆寫 Windows 註冊表中**的第一個 RowHasNames**設定,逐個檔。  
  
 還可以確定欄位的數據類型。 使用**MaxScanRows**選項指示在確定列類型時應掃描多少行。 如果將**MaxScanRows**設置為 0,則掃描整個檔。 架構中的**MaxScanRows**設置將覆蓋 Windows 註冊表中的設置,按文件進行。  
  
 以下項目指示 Microsoft Jet 應使用表第一行中的資料來確定欄位名稱,並應檢查整個檔案以確定使用的資料型態:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 下一個項目使用欄號 **(Col**_n)_ 選項指定表中的欄位,該選項對於字元分隔檔是可選的,並且固定長度檔是必需的。 此範例顯示了兩個字段的 Schema.ini 條目,一個 10 個字元的客戶編號文字欄位和一個 30 個字元的客戶名稱文字欄位:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 **Col**_n_的語法是:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>備註  
 下表描述了**Col**_n_條目的每個部分。  
  
|參數|描述|  
|---------------|-----------------|  
|*ColumnName*|列的文字名稱。 如果列名稱包含嵌入空格,則必須將其以雙引弧括在一起。|  
|*型別*|資料類型如下:<br /><br /> **Microsoft Jet 資料類型**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> long<br /><br /> 貨幣<br /><br /> Single<br /><br /> Double<br /><br /> Datetime<br /><br /> Text<br /><br /> 備忘錄<br /><br /> **ODBC 資料類型**字元(與文字相同)<br /><br /> 浮動(與雙花相同)<br /><br /> 整數(與短數相同)<br /><br /> 長字元(與備忘錄相同)<br /><br /> *日期格式*|  
|**寬度**|文字字串值`Width`。 指示以下數位指定列的寬度(對於字元分隔檔可選;固定長度檔需要)。|  
|*#*|指定列寬度的整數值(如果指定**了"寬度**",則需要)。|  
  
## <a name="selecting-a-character-set"></a>選擇字元集  
 您可以從兩個字元集中選擇:ANSI 和 OEM。 架構中的**字元集**設置將覆蓋 Windows 註冊表中的設置,逐個檔。 下面的範例顯示了將字元設定為 ANSI 的架構.ini 條目:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>指定資料型態格式和轉換  
 Schema.ini 檔包含多個選項,可用於指定數據的轉換或顯示方式。 下表列出了每個選項。  
  
|選項|描述|  
|------------|-----------------|  
|**DateTimeFormat**|可以設置為指示日期和時間的格式字串。 如果導入/匯出中的所有日期/時間欄位都使用相同的格式處理,則應指定此條目。 除 A.M. 外,所有 Microsoft Jet 格式 與下午 。 如果沒有格式字串,則使用 Windows 控制面板短日期圖片和時間選項。|  
|**十進位元號**|可以設置為用於將整數與數位的小數部分分隔的任何單個字元。|  
|**數位位數**|指示數字小數部分中的小數位數。|  
|**數字領先零**|指定小於 1 和小於 -1 的小數值是否應包含前導零;如果十進位值小於 1,小於 -1 值是否應包含前導零。此值可以是 False(無前導零)或 True。|  
|**CurrencySymbol**|指示可用於文本檔中貨幣值的貨幣符號。 範例包括美元符號 ($) 和 Dm。|  
|**貨幣貨幣格式**|可以設定為以下的任何值:<br /><br /> - 無分隔的貨幣符號前置字串 ($1)<br />- 貨幣符號後綴,無分離 (1$)<br />- 帶有一個字元分隔的貨幣符號前置字串 ($ 1)<br />- 帶有一個字元分隔(1 美元)的貨幣符號後綴|  
|**貨幣數字**|指定用於貨幣金額小數部分的數字數。|  
|**貨幣內格羅格式**|可以是下列其中一個值：<br /><br /> - (1美元)<br />- -$1<br />- $-1<br />- $1-<br />- (1美元)<br />- -1$<br />- 1-$<br />- 1美元-<br />- -1 $<br />- -$ 1<br />- 1 $-<br />- $ 1-<br />- $ -1<br />- 1- $<br />- (1美元)<br />- (1 $)<br /><br /> 此示例顯示美元符號,但應在實際程式中將其替換為相應的**貨幣符號**值。|  
|**貨幣千符號**|指示可用於將文本檔中的貨幣值分隔成千計的單字元符號。|  
|**貨幣十進位元號**|可以設置為任何單個字元,用於將整體與貨幣金額的小數部分分開。|  
  
> [!NOTE]  
>  如果省略了項,則使用 Windows 控制面板中的預設值。
