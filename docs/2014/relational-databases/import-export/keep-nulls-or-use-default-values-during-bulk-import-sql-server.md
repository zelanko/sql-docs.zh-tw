---
title: 大量匯入期間保留 Null 或使用預設值 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5999a7f3a952cd0392136a96bf3bf166c8e6b155
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011896"
---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>大量匯入期間保留 Null 或使用預設值 (SQL Server)
  根據預設，當資料匯入資料表時， **bcp** 命令和 BULK INSERT 陳述式會查看資料表中的資料行是否已定義預設值。 例如，若資料檔中有一個 Null 值欄位，將會以載入該資料行的預設值來取代。 **bcp** 命令和 BULK INSERT 陳述式都可讓您指定保留 Null 值。  
  
 相對地，一般的 INSERT 陳述式會保留 Null 值，而不會插入預設值。 INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式所提供的基本行為與一般 INSERT 陳述式相同，但它還支援用於插入預設值的資料表提示。  
  
> [!NOTE]  
>  如需略過資料表資料行的範例格式檔案，請參閱[使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)。  
  
## <a name="sample-table-and-data-file"></a>範例資料表與資料檔  
 若要執行此主題中的範例，您必須建立範例資料表與資料檔。  
  
### <a name="sample-table"></a>範例資料表  
 在此範例中，必須將名為 **MyTestDefaultCol2** 的資料表，建立在 **AdventureWorks** 範例資料庫中的 **dbo** 結構描述下。 若要建立此資料表， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]請在 [查詢編輯器] 中執行：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE MyTestDefaultCol2   
(Col1 smallint,  
Col2 nvarchar(50) DEFAULT 'Default value of Col2',  
Col3 nvarchar(50)   
);  
GO  
  
```  
  
 請注意，第二個資料表資料行 `Col2` 中有預設值。  
  
### <a name="sample-format-file"></a>範例格式檔案  
 有些大量匯入範例會使用非 XML 格式檔案 `MyTestDefaultCol2-f-c.Fmt`，此檔案與 `MyTestDefaultCol2` 資料表完全對應。 若要建立此格式檔案，請在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示字元下，輸入：  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 format nul -c -f C:\MyTestDefaultCol2-f-c.Fmt -t, -r\n -T  
  
```  
  
 如需建立格式檔案的詳細資訊，請參閱 [建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)。  
  
### <a name="sample-data-file"></a>範例資料檔  
 此範例將使用範例資料檔 `MyTestEmptyField2-c.Dat`，此檔案在第二個欄位中不含任何值。 `MyTestEmptyField2-c.Dat` 資料檔含有下列記錄。  
  
```  
1,,DataField3  
2,,DataField3  
  
```  
  
## <a name="keeping-null-values-with-bcp-or-bulk-insert"></a>使用 bcp 或 BULK INSERT 保留 Null 值  
 下列限定詞 (qualifier) 可指定資料檔中的空白欄位，在大量匯入作業期間保留其 Null 值，而不要繼承資料表資料行的預設值 (若有的話)。  
  
|Command|Qualifier|限定詞類型|  
|-------------|---------------|--------------------|  
|**bcp**|`-k`|Switch|  
|BULK INSERT|KEEPNullS<sup>1</sup>|引數|  
  
 <sup>1</sup>針對 BULK INSERT，如果無法使用預設值，則必須將資料表資料行定義為允許 null 值。  
  
> [!NOTE]  
>  這些限定詞會使這些大量匯入命令不再檢查資料表上有無 DEFAULT 定義， 但對任何並行 INSERT 陳述式而言，DEFAULT 定義是可預期的。  
  
 如需詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)和 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
### <a name="examples"></a>範例  
 本節中的範例使用 **bcp** 或 BULK INSERT 進行大量匯入，並保留 Null 值。  
  
 第二個資料表資料行 **Col2** 有預設值。 資料檔的對應欄位包含空白字串。 依預設，若使用 **bcp** 或 BULK INSERT 將資料由此資料檔匯入 **MyTestDefaultCol2** 資料表中，則會插入預設值 **Col2**，進而產生下列結果：  
  
||||  
|-|-|-|  
|`1`|`Default value of Col2`|`DataField3`|  
|`2`|`Default value of Col2`|`DataField3`|  
  
 若要插入`NULL`"" 而非`Default value of Col2`""，您必須使用`-k` switch 或 KEEPNull 選項，如下列**bcp**和 BULK INSERT 範例所示。  
  
#### <a name="using-bcp-and-keeping-null-values"></a>使用 bcp 並保留 Null 值  
 下列範例示範如何使用 **bcp** 命令保留 Null 值。 **Bcp**命令包含下列參數：  
  
|Switch|描述|  
|------------|-----------------|  
|`-f`|指定命令將使用格式檔案。|  
|`-k`|指定空白資料行在作業過程中應保持 Null 值，而非保有插入之資料行的任何預設值。|  
|`-T`|指定以信任連接將 bcp 公用程式連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
  
 在 Windows 命令提示字元中，輸入：  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 in C:\MyTestEmptyField2-c.Dat -f C:\MyTestDefaultCol2-f-c.Fmt -k -T  
  
```  
  
#### <a name="using-bulk-insert-and-keeping-null-values"></a>使用 BULK INSERT 並保留 Null 值  
 以下範例將示範如何在 BULK INSERT 陳述式中使用 KEEPNULLS 選項。 從查詢工具 (例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器) 執行：  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT MyTestDefaultCol2  
   FROM 'C:\MyTestEmptyField2-c.Dat'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      KEEPNULLS  
   );  
GO  
  
```  
  
## <a name="keeping-default-values-with-insert--select--from-openrowsetbulk"></a>保留預設值與 INSERT .。。SELECT * FROM OPENROWSET （BULK ...）  
 根據預設，在大量載入作業中未指定的任何資料行都會設定為 Null，方法是使用 INSERT .。。SELECT * FROM OPENROWSET （BULK ...）。不過，您可以針對資料檔中的空白欄位指定，對應的資料表資料行會使用其預設值（如果有的話）。 若要使用預設值，請指定下列資料表提示：  
  
|Command|Qualifier|限定詞類型|  
|-------------|---------------|--------------------|  
|INSERT ...SELECT * FROM OPENROWSET(BULK...)|WITH(KEEPDEFAULTS)|資料表提示|  
  
> [!NOTE]  
>  如需詳細資訊，請參閱[INSERT &#40;transact-sql&#41;](/sql/t-sql/statements/insert-transact-sql)、 [SELECT &#40;Transact-sql&#41;](/sql/t-sql/queries/select-transact-sql)、 [OPENROWSET &#40;transact-sql&#41;](/sql/t-sql/functions/openrowset-transact-sql)和[Table 提示 &#40;transact-sql&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
### <a name="examples"></a>範例  
 下列插入 .。。SELECT * FROM OPENROWSET （BULK ...）範例會大量匯入資料並保留預設值。  
  
 若要執行範例，您必須建立 **MyTestDefaultCol2** 範例資料表與 `MyTestEmptyField2-c.Dat` 資料檔，並使用格式檔案 `MyTestDefaultCol2-f-c.Fmt`。 如需建立這些範例的詳細資訊，請參閱本主題稍早的「範例資料表與資料檔」。  
  
 第二個資料表資料行 **Col2** 有預設值。 資料檔的對應欄位包含空白字串。 當 INSERT .。。SELECT \* FROM OPENROWSET （BULK ...）將此資料檔的欄位匯入**MyTestDefaultCol2**資料表中，根據預設，Null 會插入至**Col2** ，而不是預設值。 此預設行為會產生下列結果：  
  
||||  
|-|-|-|  
|`1`|`NULL`|`DataField3`|  
|`2`|`NULL`|`DataField3`|  
  
 若要插入預設值 "`Default value of Col2`" 而非 "`NULL`"，您必須使用 KEEPDEFAULTS 資料表提示，如下列範例所示。 從查詢工具 (例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器) 執行：  
  
```  
USE AdventureWorks;  
GO  
INSERT INTO MyTestDefaultCol2  
    WITH (KEEPDEFAULTS)  
    SELECT *  
      FROM OPENROWSET(BULK  'C:\MyTestEmptyField2-c.Dat',  
      FORMATFILE='C:\MyTestDefaultCol2-f-c.Fmt'       
      ) as t1 ;  
GO  
  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [大量匯入資料時保留識別值 &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [準備大量匯出或匯入的資料 &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **若要使用格式檔案**  
  
-   [建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **若要在使用 bcp 時指定相容性的資料格式**  
  
-   [指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [使用 bcp 指定資料檔的前置長度 &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [使用 bcp 時指定檔案儲存類型 &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [資料表提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
