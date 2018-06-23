---
title: 使用 BCP 指定檔案儲存類型 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 68630ac6e4a2ffad9079ed620e8d7d9660bf6381
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031628"
---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>使用 bcp 指定檔案儲存類型 (SQL Server)
  *檔案儲存類型* 描述資料如何儲存在資料檔中。 資料可以匯出到資料檔案做為其資料庫資料表類型 （原生格式）、 依其字元表示 （字元格式），或為支援隱含轉換的位置; 任何資料類型例如，複製`smallint`為`int`。 使用者自訂資料類型會依其基底類型匯出。  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>檔案儲存類型的 bcp 提示  
 如果互動式 **bcp** 命令包含 **in** 或 **out** 選項，但沒有格式檔案參數 (**-f**) 或資料格式參數 (**-n**、 **-c**、 **-w**或 **-N**)，此命令就會提示您輸入每個資料欄位的檔案儲存類型，如下所示：  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 您對此提示的回應視執行的工作而定，如下所示：  
  
-   若要以最精簡的儲存方式 (原生資料格式) 將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料大量匯出到資料檔案，請接受 **bcp**提供的預設檔案儲存類型。 如需原生檔案儲存類型的清單，請參閱此主題稍後的＜原生檔案儲存類型＞。  
  
-   執行個體的資料大量匯出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字元格式資料檔，以指定`char`作為檔案儲存類型的資料表中的所有資料行。  
  
-   執行個體的資料大量匯入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]從資料檔中，將檔案儲存類型指定為`char`以字元會格式化，並以原生資料類型格式儲存的資料，指定檔案儲存類型的其中一個適當地：  
  
    |檔案儲存類型|在命令提示字元中輸入|  
    |-----------------------|-----------------------------|  
    |`char` <sup>1</sup>|`c`[`har`]|  
    |`varchar`|`c[har]`|  
    |`nchar`|`w`|  
    |`nvarchar`|`w`|  
    |`text` <sup>2</sup>|`T`[`ext`]|  
    |`ntext2`|`W`|  
    |`binary`|`x`|  
    |`varbinary`|`x`|  
    |`image` <sup>2</sup>|`I`[`mage`]|  
    |`datetime`|**d[ate]**|  
    |`smalldatetime`|`D`|  
    |`time`|`te`|  
    |`date`|`de`|  
    |`datetime2`|`d2`|  
    |`datetimeoffset`|`do`|  
    |`decimal`|`n`|  
    |`numeric`|`n`|  
    |`float`|**f[loat]**|  
    |`real`|`r`|  
    |`Int`|**i[nt]**|  
    |`bigint`|`B[igint]`|  
    |`smallint`|**s[mallint]**|  
    |`tinyint`|**t[inyint]**|  
    |`money`|**m[oney]**|  
    |`smallmoney`|`M`|  
    |`bit`|`b[it]`|  
    |`uniqueidentifier`|`u`|  
    |`sql_variant`|`V[ariant]`|  
    |`timestamp`|`x`|  
    |`UDT` (使用者定義的資料類型)|`U`|  
    |`XML`|`X`|  
  
     <sup>1</sup>欄位長度、 前置長度及結束字元的互動，可決定配置給非字元資料的匯出為資料檔中的儲存空間量`char`檔案儲存類型。  
  
     <sup>2</sup> `ntext`， `text`，和`image`的未來版本將移除的資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些資料類型，並規劃修改目前使用這些資料類型的應用程式。 使用`nvarchar(max)`， `varchar(max)`，和`varbinary(max)`改為。  
  
## <a name="native-file-storage-types"></a>原生檔案儲存類型  
 每個原生檔案儲存類型都記錄於格式檔案內，做為對應的主機檔案資料類型。  
  
|檔案儲存類型|主檔案資料類型|  
|-----------------------|-------------------------|  
|`char` <sup>1</sup>|SQLCHAR|  
|`varchar`|SQLCHAR|  
|`nchar`|SQLNCHAR|  
|`nvarchar`|SQLNCHAR|  
|`text` <sup>2</sup>|SQLCHAR|  
|`ntext` <sup>2</sup>|SQLNCHAR|  
|`binary`|SQLBINARY|  
|`varbinary`|SQLBINARY|  
|`image` <sup>2</sup>|SQLBINARY|  
|`datetime`|SQLDATETIME|  
|`smalldatetime`|SQLDATETIM4|  
|`decimal`|SQLDECIMAL|  
|`numeric`|SQLNUMERIC|  
|`float`|SQLFLT8|  
|`real`|SQLFLT4|  
|`int`|SQLINT|  
|`bigint`|SQLBIGINT|  
|`smallint`|SQLSMALLINT|  
|`tinyint`|SQLTINYINT|  
|`money`|SQLMONEY|  
|`smallmoney`|SQLMONEY4|  
|`bit`|SQLBIT|  
|`uniqueidentifier`|SQLUNIQUEID|  
|`sql_variant`|SQLVARIANT|  
|`timestamp`|SQLBINARY|  
|UDT (使用者定義資料類型)|SQLUDT|  
  
 <sup>1</sup>格式資料檔案儲存在字元採用`char`做為檔案儲存類型。 因此，對於字元資料檔案，SQLCHAR 是唯一會出現在格式檔案中的資料類型。  
  
 <sup>2</sup>您無法將大量資料匯入`text`， `ntext`，和`image`資料行的預設值。  
  
## <a name="additional-considerations-for-file-storage-types"></a>檔案儲存類型的額外考量  
 當您將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料大量匯出到資料檔案時：  
  
-   您永遠可以將檔案儲存類型指定為 `char`。  
  
-   如果您輸入檔案儲存類型代表無效的隱含轉換， **bcp**失敗; 例如，雖然您可以指定`int`的`smallint`資料，如果您指定`smallint`如`int`資料，導致溢位錯誤。  
  
-   當非字元資料類型例如`float`， `money`， `datetime`，或`int`會儲存為其資料庫類型時，將資料寫入資料檔中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生格式。  
  
    > [!NOTE]  
    >  以互動方式在 **bcp** 命令中指定所有欄位之後，此命令會提示您將每個欄位的回應以非 XML 格式的檔案加以儲存。 如需非 XML 格式檔案的詳細資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [使用 bcp 指定欄位長度 &#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)   
 [指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [使用 bcp 指定資料檔的前置長度 &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
