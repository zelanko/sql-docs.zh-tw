---
title: 使用 BCP 指定欄位長度 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- default field lengths
- field length [SQL Server]
- data formats [SQL Server], field length
- bcp utility [SQL Server], field length
ms.assetid: 240f33ca-ef4a-413a-a4de-831885cb505b
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5bda4afe1b3c6b64ea1609412be66de03fa6329e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32940143"
---
# <a name="specify-field-length-by-using-bcp-sql-server"></a>使用 bcp 指定欄位長度 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  欄位長度會指出以字元格式表現資料所需的最大字元數。 如果資料是以原生格式儲存，則欄位長度為已知；例如， **int** 資料類型會佔用 4 個位元組。 如果指出前置長度為 0， **bcp** 命令就會提示您輸入欄位長度 (預設的欄位長度)，以及欄位長度對包含 **char** 資料之資料檔案的資料儲存有何影響。  
  
## <a name="the-bcp-prompt-for-field-length"></a>bcp 提示輸入欄位長度  
 如果互動式 **bcp** 命令包含 **in** 或 **out** 選項，但沒有格式檔案參數 (**-f**) 或資料格式參數 (**-n**、**-c**、**-w** 或 **-N**)，此命令就會提示您輸入每個資料欄位的欄位長度，如下所示：  
  
 `Enter length of field <field_name> [<default>]:`  
  
 如需在內容中顯示此提示的範例，請參閱 [使用 bcp 指定相容性的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)。  
  
> [!NOTE]  
>  以互動方式在 **bcp** 命令中指定所有欄位之後，此命令會提示您將每個欄位的回應以非 XML 格式的檔案加以儲存。 如需非 XML 格式檔案的詳細資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)。  
  
 **bcp** 命令是否會提示輸入欄位長度，取決於以下數個因素：  
  
-   當您複製的資料類型沒有固定長度，而且指定前置長度為 0 時， **bcp** 就會提示輸入欄位長度。  
  
-   將非字元資料轉換為字元資料時， **bcp** 會建議足以儲存資料的預設欄位長度。  
  
-   如果是非字元的檔案儲存類型， **bcp** 命令就不會提示輸入欄位長度。 該資料會以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生資料表示法 (原生格式) 儲存。  
  
## <a name="using-default-field-lengths"></a>使用預設的欄位長度  
 一般而言， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您接受 **bcp**所建議的欄位長度預設值。 已建立字元模式資料檔案時，使用預設的欄位長度可確定不會截斷資料，而且不會發生數值溢位錯誤。  
  
 如果指定不正確的欄位長度，就會發生問題。 例如，如果複製數值資料，而對該資料來說指定的欄位長度太短， **bcp** 公用程式就會印出溢位訊息，而且不會複製該資料。 此外，若要匯出 **datetime** 資料，而且指定給字元字串的欄位長度少於 26 個位元組，則 **bcp** 公用程式會直接截斷資料而不會發出錯誤訊息。  
  
> [!IMPORTANT]  
>  使用預設的大小選項時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預期會讀取整個字串。 在某些狀況下，使用預設欄位長度卻會導致發生「未預期的檔案結尾」錯誤。 一般來說，當資料檔案中只有部分預期的欄位出現時， **money** 與 **datetime** 資料類型可能會發生此錯誤；例如，指定 **mm** dd *yy*/*的*/*datetime* 值而未指定時間元件時，就會比 **char** 格式的 **datetime** 值所預期的 24 個字元長度要短。 若要避免此種錯誤類型，請使用欄位結束字元或固定長度資料欄位，或指定其他的值以變更預設的欄位長度。  
  
### <a name="default-field-lengths-for-character-file-storage"></a>字元檔案儲存的預設欄位長度  
 下表列出資料的預設欄位長度，以儲存為字元檔案儲存類型。 可為 Null 的資料長度與非 Null 的資料長度相同。  
  
|資料類型|預設長度 (字元)|  
|---------------|-----------------------------------|  
|**char**|該資料行的定義長度|  
|**varchar**|該資料行的定義長度|  
|**nchar**|該資料行定義長度的兩倍|  
|**nvarchar**|該資料行定義長度的兩倍|  
|**Text**|0|  
|**ntext**|0|  
|**bit**|@shouldalert|  
|**binary**|該資料行定義長度的兩倍 + 1|  
|**varbinary**|該資料行定義長度的兩倍 + 1|  
|**image**|0|  
|**datetime**|24|  
|**smalldatetime**|24|  
|**float**|30|  
|**real**|30|  
|**int**|12|  
|**bigint**|19|  
|**smallint**|7|  
|**tinyint**|5|  
|**money**|30|  
|**smallmoney**|30|  
|**decimal**|41*|  
|**numeric**|41*|  
|**uniqueidentifier**|37|  
|**timestamp**|17|  
|**varchar(max)**|0|  
|**varbinary(max)**|0|  
|**nvarchar(max)**|0|  
|UDT|使用者自訂術語 (UDT) 資料行的長度|  
|XML|0|  
  
 \*如需**小數點**和**數值**資料類型的詳細資訊，請參閱[小數點和數值 &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)。  
  
> [!NOTE]  
>  **tinyint** 類型的資料行可包含 0 到 255 的數值；因此代表該範圍內任意數值所需的最大字元數為 3 (代表數值 100 到 255)。  
  
### <a name="default-field-lengths-for-native-file-storage"></a>原生檔案儲存的預設欄位長度  
 下表列出資料的預設欄位長度，以儲存為原生檔案儲存類型。 可為 Null 的資料長度與非 Null 的資料長度相同，字元資料永遠都會以字元格式儲存。  
  
|資料類型|預設長度 (字元)|  
|---------------|-----------------------------------|  
|**bit**|@shouldalert|  
|**binary**|該資料行的定義長度|  
|**varbinary**|該資料行的定義長度|  
|**image**|0|  
|**datetime**|8|  
|**smalldatetime**|4|  
|**float**|8|  
|**real**|4|  
|**int**|4|  
|**bigint**|8|  
|**smallint**|2|  
|**tinyint**|@shouldalert|  
|**money**|8|  
|**smallmoney**|4|  
|**decimal**|*|  
|**numeric**|*|  
|**uniqueidentifier**|16|  
|**timestamp**|8|  
  
 \*如需**小數點**和**數值**資料類型的詳細資訊，請參閱[小數點和數值 &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)。  
  
 在先前的所有案例中，若要建立一個資料檔案，之後重新載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以將所佔用的儲存空間保持在最低，請搭配預設的檔案儲存類型與預設的欄位長度和長度前置詞一起使用。  
  
## <a name="see-also"></a>另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [指定欄位與資料列結束字元 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)   
 [使用 bcp 指定資料檔的前置長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [使用 bcp 指定檔案儲存類型 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)   
 [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
  
