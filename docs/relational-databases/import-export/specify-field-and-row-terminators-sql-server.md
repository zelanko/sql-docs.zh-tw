---
title: "指定欄位與資料列結束字元 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], terminators
- field terminators [SQL Server]
- data formats [SQL Server], terminators
- row terminators [SQL Server]
- terminators [SQL Server]
ms.assetid: f68b6782-f386-4947-93c4-e89110800704
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 42c2ee3fe98d6c6fc35d2417469bc3eec9fddd8c
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="specify-field-and-row-terminators-sql-server"></a>指定欄位與資料列結束字元 (SQL Server)
  針對字元資料欄位，選擇性結束字元可讓您使用「欄位結束字元」標示資料檔案中每個欄位的結尾，並使用「資料列結束字元」標示每個資料列的結尾。 結束字元是指示程式從欄位或資料列結束與開始的交接處讀取資料檔的一種方法。  
  
> [!IMPORTANT]  
>  在使用原生或 Unicode 原生格式時，請使用長度前置詞，而不使用欄位結束字元。 由於原生格式資料檔案存放格式為 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的內部二進位資料格式，因此原生格式資料可能會與結束字元相衝突。  
  
## <a name="characters-supported-as-terminators"></a>支援為結束字元的字元  
 **bcp** 命令、BULK INSERT 陳述式與 OPENROWSET 大量資料列集提供者，都支援使用各式字元作為欄位或資料列結束字元，且一律會尋找每個結束字元的第一個執行個體。 下表列出支援作為結束字元的字元。  
  
|結束字元|表示方式|  
|---------------------------|------------------|  
|索引標籤|\t<br /><br /> 這是預設欄位結束字元。|  
|新行字元 (Newline Character)|\n<br /><br /> 這是預設資料列結束字元。|  
|歸位字元/換行字元|\r|  
|反斜線*|\\\|  
|Null 結束字元 (看不見的結束字元)**|\0|  
|任何可列印的字元 (除了 Null 值、定位點、新行字元和 Return 鍵外，控制字元均無法列印)|(*、A、t、l 等等)|  
|最多包含 10 個可列印字元的字串，包括先前所列的一些或所有結束字元|(**\t\*\*、end、!!!!!!!!!!、\t—\n 等等)|  
  
 *只有 t、n、r、0 和 '\0' 字元可以與反斜線逸出字元搭配使用，以產生控制字元。  
  
 **雖然列印時看不到 null 控制字元 (\0)，這個字元仍是資料檔中的個別字元。 這表示使用 null 控制字元做為欄位或資料列結束字元，和完全沒有欄位或資料列結束字元不同。  
  
> [!IMPORTANT]  
>  如果在資料內發現結束字元，它會當作結束字元而非當作資料來解譯，而該字元之後的資料則會解譯為屬於下一個欄位或記錄。 因此，請小心選擇結束字元，確定這些結束字元絕不會出現在您的資料中。 例如，如果資料中包含低 Surrogate，此低 surrogate 欄位結束字元就不是欄位結束字元的好選項。  
  
## <a name="using-row-terminators"></a>使用資料列結束字元  
 資料列結束字元可以和最後一個欄位的結束字元相同。 不過，個別的資料列結束字元通常十分有用。 例如，若要產生表格式輸出，請以新行字元 (\n) 結束每個資料列的最後一個欄位，並以定位字元 (Tab) 結束所有其他欄位。 若要將每個資料記錄放在資料檔中自己的那一行，請指定 \r\n 組合做為資料列結束字元。  
  
> [!NOTE]  
>  以互動方式使用 **bcp** 並指定 \n (新行) 作為資料列結束字元時， **bcp** 會自動以 \r (歸位字元) 字元當作前置詞，而產生資料列結束字元 \r\n。  
  
## <a name="specifying-terminators-for-bulk-export"></a>指定大量匯出的結束字元  
 當您大量匯出 **char** 或 **nchar** 資料，而且想要使用非預設的結束字元時，就必須對 **bcp** 命令指定結束字元。 您可以使用下列方式指定結束字元：  
  
-   使用格式檔案，按個別欄位逐一指定結束字元。  
  
    > [!NOTE]  
    >  如需格式檔案的詳細資訊，請參閱[匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)。  
  
-   不使用格式檔案，可使用下列替代方法：  
  
    -   使用 **-t** 參數，對資料列中最後一個欄位以外的所有欄位，指定欄位結束字元，並使用 **-r** 參數指定資料列結束字元。  
  
    -   使用字元格式參數 (**-c** 或 **-w**) 但不使用 **-t** 參數，會將欄位結束字元設定為定位字元 \t。 這與指定 **-t**\t 相同。  
  
        > [!NOTE]  
        >  如果您指定 **-n** (原生資料) 或 **-N** (Unicode 原生) 參數，則不會插入結束字元。  
  
    -   如果互動式 **bcp** 命令包含 **in** 或 **out** 選項，但不使用格式檔案參數 (**-f**) 或資料格式參數 (**-n**、 **-c**、 **-w**，或 **-N**)，而且您選擇不指定前置長度與欄位長度，則該命令會提示輸入每個欄位的欄位結束字元 (預設是無)：  
  
         `Enter field terminator [none]:`  
  
         預設值通常是適合的選擇。 不過，有關 **char** 或 **nchar** 資料欄位，請參閱以下「使用結束字元的指導方針」細項。 如需在內容中顯示此提示的範例，請參閱[使用 bcp 時指定相容性的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)。  
  
        > [!NOTE]  
        >  以互動方式在 **bcp** 命令中指定所有欄位之後，此命令會提示您將每個欄位的回應以非 XML 格式的檔案加以儲存。 如需非 XML 格式檔案的詳細資訊，請參閱[非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)。  
  
### <a name="guidelines-for-using-terminators"></a>使用結束字元的指導方針  
 在某些情況中，結束字元對 **char** 或 **nchar** 資料欄位而言很有用。 例如：  
  
-   資料檔中的資料行包含 Null 值，而此資料檔將要匯入至不了解前置長度資訊的程式。  
  
     包含 Null 值的任何資料行會被視為可變長度。 如果沒有使用前置長度，則需要結束字元識別 Null 欄位結尾並確定已正確解譯資料。  
  
-   許多資料列只使用其部分空間的固定長度長資料行。  
  
     在這種狀況下，指定結束字元可縮小儲存空間，允許欄位視為可變長度欄位。  
  
### <a name="examples"></a>範例  
 此範例會使用字元格式、以逗號作為欄位結束字元，而且以新行字元 (\n) 作為資料列結束字元，將資料從 `AdventureWorks.HumanResources.Department` 資料表大量匯出資料至 `Department-c-t.txt` 資料檔案。  
  
 **bcp** 命令包含下列參數。  
  
|參數|描述|  
|------------|-----------------|  
|**-c**|指定以字元資料載入資料欄位。|  
|**-t** `,`|指定逗號 (,) 做為欄位結束字元。|  
|**-r** \n|指定資料列結束字元為新行字元。 此為預設資料列結束字元，因此可選擇性地加以指定。|  
|**-T**|指定 **bcp** 公用程式使用整合式安全性的信任連接，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，則必須指定 **-U** 與 **-P** ，才能順利登入。|  
  
 如需相關資訊，請參閱 [bcp Utility](../../tools/bcp-utility.md)。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示字元中，輸入：  
  
```  
bcp AdventureWorks.HumanResources.Department out C:\myDepartment-c-t.txt -c -t, -r \n -T  
```  
  
 這會建立 `Department-c-t.txt`，四個欄位中各包含 16 筆記錄。 這些欄位會以逗號隔開。  
  
## <a name="specifying-terminators-for-bulk-import"></a>指定大量匯入的結束字元  
 當您大量匯入 **char** 或 **nchar** 資料時，大量匯入命令必須辨識資料檔案中使用的結束字元。 指定結束字元的方式取決於大量匯入命令，如下所示：  
  
-   **bcp**  
  
     指定匯入作業結束字元所使用的語法，與用於匯出作業的語法相同。 如需詳細資訊，請參閱本主題前面的「指定大量匯出的結束字元」。  
  
-   BULK INSERT  
  
     您可以使用下表所示的限定詞，針對格式檔案中的個別欄位或整個資料檔指定結束字元。  
  
    |Qualifier|描述|  
    |---------------|-----------------|  
    |FIELDTERMINATOR **='***field_terminator***'**|指定要用於字元和 Unicode 字元資料檔中的欄位結束字元。<br /><br /> 預設值是 \t (定位字元)。|  
    |ROWTERMINATOR **='***row_terminator***'**|指定要用於字元和 Unicode 字元資料檔中的資料列結束字元。<br /><br /> 預設值是 \n (新行字元)。|  
  
     如需詳細資訊，請參閱 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)。  
  
-   INSERT ...SELECT * FROM OPENROWSET(BULK...)  
  
     針對 OPENROWSET 大量資料列集提供者，只可以在格式檔案中指定結束字元 (除了大型物件資料類型以外都需要格式檔案)。 如果字元資料檔使用非預設結束字元，則必須在格式檔案中加以定義。 如需詳細資訊，請參閱[建立格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md) 和[使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)。  
  
     如需有關 OPENROWSET BULK 子句的詳細資訊，請參閱 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)。  
  
### <a name="examples"></a>範例  
 這一節中的範例會將字元資料從先前範例中建立的 `Department-c-t.txt` 資料檔，大量匯入到 `myDepartment` 範例資料庫中的 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料表。 您必須先建立這個資料表，才能執行範例。 在 **dbo** 結構描述下建立這個資料表時，請在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中執行下列程式碼：  
  
```tsql  
USE AdventureWorks;  
GO  
DROP TABLE myDepartment;  
CREATE TABLE myDepartment   
(DepartmentID smallint,  
Name nvarchar(50),  
GroupName nvarchar(50) NULL,  
ModifiedDate datetime not NULL CONSTRAINT DF_AddressType_ModifiedDate DEFAULT (GETDATE())  
);  
GO 
```  
  
#### <a name="a-using-bcp-to-interactively-specify-terminators"></a>A. 使用 bcp 以互動方式指定結束字元  
 下列範例會使用 `Department-c-t.txt` 命令，大量匯入 `bcp` 資料檔。 此命令與大量匯出命令使用相同的命令參數。 如需詳細資訊，請參閱本主題前面的「指定大量匯出的結束字元」。  
  
 在 Windows 命令提示字元上輸入：  
  
```  
bcp AdventureWorks..myDepartment in C:\myDepartment-c-t.txt -c -t , -r \n -T  
```  
  
#### <a name="b-using-bulk-insert-to-interactively-specify-terminators"></a>B. 使用 BULK INSERT 以互動方式指定結束字元  
 下列範例會使用 `Department-c-t.txt` 陳述式 (其中使用下表所示的限定詞)，大量匯入 `BULK INSERT` 資料檔。  
  
|選項|Attribute|  
|------------|---------------|  
|DATAFILETYPE **='**char**'**|指定以字元資料載入資料欄位。|  
|FIELDTERMINATOR **='**`,`**'**|指定逗號 (`,`) 作為欄位結束字元。|  
|ROWTERMINATOR **='**`\n`**'**|指定資料列結束字元為新行字元。|  
  
 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行下列程式碼：  
  
```tsql  
USE AdventureWorks;  
GO  
BULK INSERT myDepartment FROM 'C:\myDepartment-c-t.txt'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      ROWTERMINATOR = '\n'  
);  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [使用 bcp 時指定欄位長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)   
 [使用 bcp 時指定資料檔案的前置長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [使用 bcp 時指定檔案儲存類型 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  

