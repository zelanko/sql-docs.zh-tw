---
title: 使用 bcp 指定相容性資料格式
description: 對於使用 bcp 在 SQL Server 中大量匯出，資料格式可能會與預期的版面配置不相容。 非 XML 格式檔案會指定相容性資料格式。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], compatibility
- bulk importing [SQL Server], compatibility
- compatibility [SQL Server], data formats
- data formats [SQL Server], compatibility
- bcp utility [SQL Server], compatibility
ms.assetid: cd5fc8c8-eab1-4165-9468-384f31e53f0a
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 9bae99e460ea8a9e5e2877917bd8a82b25f8cc8a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001132"
---
# <a name="specify-compatibility-data-formats-when-using-bcp-sql-server"></a>在使用 bcp 時指定相容性資料格式 (SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  此主題描述資料格式屬性、欄位特定提示，以及以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**bcp** 命令的非 XML 格式檔案來儲存逐欄位資料。 大量匯出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料以大量匯入至另一個程式 (例如另一個資料庫程式) 時，了解這些資訊十分有用。 在來源資料表中的預設資料格式 (原生、字元或 Unicode) 可能和另一個程式所預期的資料配置不相容。如果匯出資料時發生了不相容的狀況，您就必須描述資料配置的方式。  
  
> [!NOTE]  
>  如不熟悉資料匯入或匯出的資料格式，請參閱 [大量匯入或大量匯出的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)。  
  
  
##  <a name="bcp-data-format-attributes"></a><a name="bcpDataFormatAttr"></a> bcp 資料格式屬性  
 **bcp** 命令可讓您根據下列資料格式屬性，指定資料檔中每個欄位的結構：  
  
-   檔案儲存類型  
  
     *檔案儲存類型* 描述資料如何儲存在資料檔中。 資料可以依其資料庫資料表類型 (原生格式)、依其字元表示 (字元格式)，或者依支援隱含轉換的任何資料類型匯出至資料檔；例如，將 **smallint** 複製為 **int**。使用者自訂資料類型會依其基底類型匯出。 如需詳細資訊，請參閱 [使用 bcp 時指定檔案儲存類型 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)。  
  
-   前置長度  
  
     為了讓原生格式的資料大量匯出至資料檔時，能夠有最精簡的檔案儲存方式， **bcp** 命令會在每個欄位前面都加上一個或多個字元，指出欄位的長度。 這些字元稱作 *「長度前置字元」* (Length prefix characters)。 如需詳細資訊，請參閱 [使用 bcp 時指定資料檔案的前置長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)。  
  
-   欄位長度  
  
     欄位長度會指出以字元格式表現資料所需的最大字元數。 如果資料是以原生格式儲存，則欄位長度為已知。 如需詳細資訊，請參閱 [使用 bcp 指定欄位長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)。  
  
-   欄位結束字元  
  
     針對字元資料欄位，選擇性的結束字元讓您可以標示資料檔中每個欄位的結尾 (使用「欄位結束字元」  )，以及每個資料列的結尾 (使用「資料列結束字元」  )。 結束字元可讓讀取資料檔的程式知道某個欄位或資料列在何處結束，另一個在何處開始。 如需詳細資訊，請參閱 [指定欄位與資料列結束字元 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)。  
  
  
##  <a name="overview-of-the-field-specific-prompts"></a><a name="FieldSpecificPrompts"></a> 欄位專用提示字元的概觀  
 如果互動式 **bcp** 命令包含 **in** 或 **out** 選項，但不包含格式檔案參數 ( **-f**) 或資料格式參數 ( **-n**、 **-c**、 **-w**或 **-N**)，則來源資料表或目標資料表中的每個資料行，會相繼出現每個先前屬性的命令提示字元。 在每個提示字元中， **bcp** 命令是根據資料表資料行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型來提供預設值。 接受所有提示字元的預設值，會和在命令行上指定原生格式 ( **-n**) 產生相同結果。 每個提示都會將預設值顯示於方括號中：[*預設值*]。 按下 ENTER 即可接受顯示的預設值。 若要指定預設以外的值，請在提示字元中輸入新值。  
  
### <a name="example"></a>範例  
 下列範例使用 **bcp** 命令，將資料以互動方式從 `HumanResources.myTeam` 資料表大量匯出至 `myTeam.txt` 檔案。 您必須先建立此資料表，才能執行範例。 如需此資料表及建立方式的相關資訊，請參閱 [HumanResources.myTeam 範例資料表 &#40;SQL Server&#41;](../../relational-databases/import-export/humanresources-myteam-sample-table-sql-server.md)。  
  
 該命令不會指定格式檔案，也不會指定資料類型，因此會導致 **bcp** 出現提示詢問資料格式資訊。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示字元中，輸入：  
  
```cmd
bcp AdventureWorks.HumanResources.myTeam out myTeam.txt -T  
```  
  
 bcp 會針對每個資料行提示欄位專用的值。 下列範例將為資料表的 `EmployeeID` 和 `Name` 資料行，顯示欄位專用的提示字元，並為每個資料行建議預設的檔案儲存類型 (原生格式)。 `EmployeeID` 和 `Name` 資料行的前置長度分別為 0 和 2。 使用者指定逗號 (`,`)，作為每個欄位的結束字元。  
  
 `Enter the file storage type of field EmployeeID [smallint]:`  
  
 `Enter prefix-length of field EmployeeID [0]:`  
  
 `Enter field terminator [none]:,`  
  
 `Enter the file storage type of field Name [nvarchar]:`  
  
 `Enter prefix length of field Name [2]:`  
  
 `Enter field terminator [none]:,`  
  
 `.`  
  
 `.`  
  
 `.`  
  
 相等的提示字元 (視需要而定) 會依序顯示在每個資料表資料行中。  
  
  
##  <a name="storing-field-by-field-data-in-a-non-xml-format-file"></a><a name="FieldByFieldNonXmlFF"></a> 將逐欄資料儲存至非 XML 格式檔案中  
 指定所有的資料表資料行之後， **bcp** 命令會提示您選擇性地產生非 XML 格式檔案，該檔案儲存剛剛提供的逐欄資訊 (請參閱先前範例)。 如果您選擇產生格式檔案，則可以隨時匯出該資料表的資料，或將類結構化資料匯入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  您可以使用格式檔案，從資料檔中將資料大量匯入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，或從資料表中大量匯出資料，而不需重新指定格式。 如需詳細資訊，請參閱 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)＞。  
  
 下列範例會建立一個名為 `myFormatFile.fmt`的非 XML 格式檔案。  
  
 `Do you want to save this format information in a file? [Y/n] y`  
  
 `Host filename: [bcp.fmt]myFormatFile.fmt`  
  
 格式檔案的預設名稱為 bcp.fmt，但您也可以選擇指定不同的檔案名稱。  
  
> [!NOTE]  
>  若為使用單一資料格式作為檔案儲存類型的資料檔 (例如字元或原生格式)，您可以快速建立格式檔案，而不需透過 [格式]  選項來匯出或匯入資料。 此方法的優點是容易使用，並且可讓您建立 XML 格式檔案或非 XML 格式檔案。 如需詳細資訊，請參閱[建立格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)。  
  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 bcp 時指定檔案儲存類型 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
-   [使用 bcp 指定資料檔的前置長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [使用 bcp 指定欄位長度 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)  
  
-   [指定欄位與資料列結束字元 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
## <a name="related-content"></a>相關內容  
 無。  
  
## <a name="see-also"></a>另請參閱  
 [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [大量匯入或大量匯出的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
