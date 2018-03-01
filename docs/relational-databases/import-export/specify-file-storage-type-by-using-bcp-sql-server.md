---
title: "使用 BCP 指定檔案儲存類型 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0b3ea3ad1c9c467925e50e4fdc337d2dd99c858b
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2018
---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>使用 bcp 指定檔案儲存類型 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
*檔案儲存類型* 描述資料如何儲存在資料檔中。 資料可以依其資料庫資料表類型 (原生格式)、依其字元表示 (字元格式)，或者依支援隱含轉換的任何資料類型匯出至資料檔；例如，將 **smallint** 複製為 **int**。使用者自訂資料類型會依其基底類型匯出。  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>檔案儲存類型的 bcp 提示  
 如果互動式 **bcp** 命令包含 **in** 或 **out** 選項，但沒有格式檔案參數 (**-f**) 或資料格式參數 (**-n**、 **-c**、 **-w**或 **-N**)，此命令就會提示您輸入每個資料欄位的檔案儲存類型，如下所示：  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 您對此提示的回應視執行的工作而定，如下所示：  
  
-   若要以最精簡的儲存方式 (原生資料格式) 將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料大量匯出到資料檔案，請接受 **bcp**提供的預設檔案儲存類型。 如需原生檔案儲存類型的清單，請參閱此主題稍後的＜原生檔案儲存類型＞。  
  
-   若要以字元格式將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料大量匯出到資料檔案，請將資料表中所有資料行的檔案儲存類型指定為 **char** 。  
  
-   若要將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料大量匯入資料檔案，請針對以字元格式儲存的類型，將檔案儲存類型指定為 **char** ；針對以原生資料類型格式儲存的資料，則指定其中一個適當的檔案儲存類型：  
  
    |檔案儲存類型|在命令提示字元中輸入|  
    |-----------------------|-----------------------------|  
    |**char***|**c**[**har**]|  
    |**varchar**|**c[har]**|  
    |**nchar**|**w**|  
    |**nvarchar**|**w**|  
    |**text***\*|**T**[**ext**]|  
    |**ntext2**|**W**|  
    |**binary**|**x**|  
    |**varbinary**|**x**|  
    |**image***\*|**I**[**mage**]|  
    |**datetime**|**d[ate]**|  
    |**smalldatetime**|**D**|  
    |**time**|**te**|  
    |**date**|**de**|  
    |**datetime2**|**d2**|  
    |**datetimeoffset**|**do**|  
    |**decimal**|**n**|  
    |**numeric**|**n**|  
    |**float**|**f[loat]**|  
    |**real**|**r**|  
    |**整數**|**i[nt]**|  
    |**bigint**|**B[igint]**|  
    |**smallint**|**s[mallint]**|  
    |**tinyint**|**t[inyint]**|  
    |**money**|**m[oney]**|  
    |**smallmoney**|**M**|  
    |**bit**|**b[it]**|  
    |**uniqueidentifier**|**u**|  
    |**sql_variant**|**V[ariant]**|  
    |**timestamp**|**x**|  
    |**UDT** (使用者定義資料類型)|**U**|  
    |**XML**|**X**|  
  
     \*欄位長度、前置長度及結束字元的互動，可決定在資料檔案中配置給非字元資料的儲存空間數量，而此資料將匯出為 **char** 檔案儲存類型。  
  
     \*\***的未來版本將會移除**ntext **、**text **及** image [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型。 請避免在新的開發工作中使用這些資料類型，並規劃修改目前使用這些資料類型的應用程式。 請改用 **nvarchar(max)**、 **varchar(max)**和 **varbinary(max)** 。  
  
## <a name="native-file-storage-types"></a>原生檔案儲存類型  
 每個原生檔案儲存類型都記錄於格式檔案內，做為對應的主機檔案資料類型。  
  
|檔案儲存類型|主檔案資料類型|  
|-----------------------|-------------------------|  
|**char***|SQLCHAR|  
|**varchar**|SQLCHAR|  
|**nchar**|SQLNCHAR|  
|**nvarchar**|SQLNCHAR|  
|**text***\*|SQLCHAR|  
|**ntext***\*|SQLNCHAR|  
|**binary**|SQLBINARY|  
|**varbinary**|SQLBINARY|  
|**image***\*|SQLBINARY|  
|**datetime**|SQLDATETIME|  
|**smalldatetime**|SQLDATETIM4|  
|**decimal**|SQLDECIMAL|  
|**numeric**|SQLNUMERIC|  
|**float**|SQLFLT8|  
|**real**|SQLFLT4|  
|**int**|SQLINT|  
|**bigint**|SQLBIGINT|  
|**smallint**|SQLSMALLINT|  
|**tinyint**|SQLTINYINT|  
|**money**|SQLMONEY|  
|**smallmoney**|SQLMONEY4|  
|**bit**|SQLBIT|  
|**uniqueidentifier**|SQLUNIQUEID|  
|**sql_variant**|SQLVARIANT|  
|**timestamp**|SQLBINARY|  
|UDT (使用者定義資料類型)|SQLUDT|  
  
 \*以字元格式儲存的資料檔案會採用 **char** 作為檔案儲存類型。 因此，對於字元資料檔案，SQLCHAR 是唯一會出現在格式檔案中的資料類型。  
  
 \*\*您無法將資料大量匯入具有 DEFAULT 值的 **text**、 **ntext**及 **image** 資料行。  
  
## <a name="additional-considerations-for-file-storage-types"></a>檔案儲存類型的額外考量  
 當您將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料大量匯出到資料檔案時：  
  
-   您一律可以將檔案儲存類型指定為 **char** 。  
  
-   如果您輸入的檔案儲存類型代表無效的隱含轉換，則 **bcp** 會失敗；例如，雖然您可以針對 **smallint** 資料指定 **int** ，但如果您針對 **int** 資料指定 **smallint** ，將導致溢位錯誤。  
  
-   若 **float**、 **money**、 **datetime**或 **int** 等非字元資料類型儲存為其資料庫類型時，資料會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生格式寫入資料檔案中。  
  
    > [!NOTE]  
    >  以互動方式在 **bcp** 命令中指定所有欄位之後，此命令會提示您將每個欄位的回應儲存為非 XML 格式檔案。 如需非 XML 格式檔案的詳細資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [使用 bcp 指定欄位長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)   
 [指定欄位與資料列結束字元 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)   
 [使用 bcp 指定資料檔的前置長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
