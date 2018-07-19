---
title: 使用 BCP 指定資料檔的前置長度 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server], prefix length
- prefix length [SQL Server]
- lengths [SQL Server], prefix characters
- data formats [SQL Server], prefix length
ms.assetid: ce32dd1a-26f1-4f61-b9fa-3f1feea9992e
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0924e829729039aec7221a8faeeff37a9e830310
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37212898"
---
# <a name="specify-prefix-length-in-data-files-by-using-bcp-sql-server"></a>使用 bcp 指定資料檔的前置長度 (SQL Server)
  為了讓原生格式的資料大量匯出至資料檔時，能夠有最精簡的檔案儲存方式， **bcp** 命令會在每個欄位前面都加上一個或多個字元，指出欄位的長度。 這些字元稱作 *「長度前置字元」*(Length prefix characters)。  
  
## <a name="the-bcp-prompt-for-prefix-length"></a>前置長度的 bcp 提示字元  
 如果互動式 **bcp** 命令包含 **in** 或 **out** 選項，但沒有格式檔案參數 (**-f**) 或資料格式參數 (**-n**、 **-c**、 **-w**或 **-N**)，此命令就會提示您輸入每個資料欄位的前置長度，如下所示：  
  
 `Enter prefix length of field <field_name> [<default>]:`  
  
 若您指定 0， **bcp** 會提示您輸入欄位的長度 (適用於字元資料類型) 或欄位結束字元 (適用於原生非字元類型)。  
  
> [!NOTE]  
>  以互動方式在 **bcp** 命令中指定所有欄位之後，此命令會提示您將每個欄位的回應以非 XML 格式的檔案加以儲存。 如需非 XML 格式檔案的詳細資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](xml-format-files-sql-server.md)。  
  
## <a name="overview-of-prefix-length"></a>前置長度的概觀  
 若要儲存欄位的前置長度，您需要有足夠的位元組來表示欄位的最大長度。 所需的位元組數目取決於檔案儲存類型、資料行的 Null 屬性，以及資料是以原生或字元格式儲存於資料檔中。 例如，`text`或是`image`資料類型需要四個前置字元來儲存欄位長度，但`varchar`資料類型則需要兩個字元。 在資料檔中，這些長度前置字元會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的內部二進位資料格式儲存。  
  
> [!IMPORTANT]  
>  在使用原生格式時，請使用長度前置詞，而不是欄位的結束字元。 原生格式資料可能會和結束字元有衝突，因為原生格式的資料檔是以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部二進位資料格式儲存。  
  
##  <a name="PrefixLengthsExport"></a> 大量匯出的前置長度  
  
> [!NOTE]  
>  您匯出欄位時，前置長度提示所提供的預設值，表示欄位最有效率的前置長度。  
  
 Null 值會以空白欄位表示。 為了指出欄位為空白 (代表 NULL)，欄位前置包含了值 -1，也就是說，至少需要一個位元組。 請注意，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表資料行允許 Null 值，則資料行需要的前置長度為 1 或更多，取決於檔案儲存類型。  
  
 當您大量匯出資料並以原生資料類型或字元格式儲存時，請使用下表所示的前置詞長度。  
  
|[SQL Server]<br /><br /> 資料類型|原生格式<br /><br /> NOT NULL|原生格式<br /><br /> NULL|字元格式<br /><br /> NOT NULL|字元格式<br /><br /> NULL|  
|------------------------------|--------------------------------|----------------------------|-----------------------------------|-------------------------------|  
|`char`|2|2|2|2|  
|`varchar`|2|2|2|2|  
|`nchar`|2|2|2|2|  
|`nvarchar`|2|2|2|2|  
|`text` <sup>1</sup>|4|4|4|4|  
|`ntext` <sup>1</sup>|4|4|4|4|  
|`binary`|2|2|2|2|  
|`varbinary`|2|2|2|2|  
|`image` <sup>1</sup>|4|4|4|4|  
|`datetime`|0|1|0|1|  
|`smalldatetime`|0|1|0|1|  
|`decimal`|1|1|1|1|  
|`numeric`|1|1|1|1|  
|`float`|0|1|0|1|  
|`real`|0|1|0|1|  
|`int`|0|1|0|1|  
|`bigint`|0|1|0|1|  
|`smallint`|0|1|0|1|  
|`tinyint`|0|1|0|1|  
|`money`|0|1|0|1|  
|`smallmoney`|0|1|0|1|  
|`bit`|0|1|0|1|  
|`uniqueidentifier`|1|1|0|1|  
|`timestamp`|1|1|1|1|  
|`varchar(max)`|8|8|8|8|  
|`varbinary(max)`|8|8|8|8|  
|UDT (使用者定義資料類型)|8|8|8|8|  
|XML|8|8|8|8|  
  
 <sup>1</sup> `ntext`， `text`，以及`image`的未來版本將移除的資料型別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些資料類型，並規劃修改目前在使用這些資料類型的應用程式。 使用`nvarchar(max)`， `varchar(max)`，和`varbinary(max)`改。  
  
##  <a name="PrefixLengthsImport"></a> 大量匯入的前置長度  
 大量匯入資料時，前置長度就是原先建立資料檔時即指定的值。 如果資料檔案不是由 **bcp** 命令所建立，則長度前置字元可能不存在。 在此狀況下，可指定 0 做為前置長度。  
  
> [!NOTE]  
>  若要在並非使用 **bcp**所建立的資料檔中指定前置長度，請使用本主題稍早在 [大量匯出的前置長度](#PrefixLengthsExport)中提供的長度。  
  
## <a name="see-also"></a>另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [使用 bcp 指定欄位長度 &#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)   
 [指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [使用 bcp 時指定檔案儲存類型 &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  
