---
title: 大量匯入資料時保留識別值 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5bb2fbd3129475c5d712cd4d1fce8bbe29ea096f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011910"
---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>大量匯入資料時保留識別值 (SQL Server)
  包含識別值的資料檔案可以大量匯入的實例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。 根據預設，會忽略所匯入資料檔案中的識別欄位值， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動指定唯一值。 唯一值的依據是資料表建立期間所指定的初始值及累加值。  
  
 如果資料檔不包含資料表中識別碼資料行的值，請使用格式檔案指定在匯入資料時應略過資料表中的識別碼資料行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動為資料行指定唯一值。  
  
 若要在將資料列大量匯入資料表時，不讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指定識別值，請使用適當的 keep-identity 命令限定詞。 當您指定 keep-identity 限定詞時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用資料檔案中的識別值。 這些限定詞如下：  
  
|Command|Keep-identity 限定詞|限定詞類型|  
|-------------|------------------------------|--------------------|  
|`bcp`|**-E**|Switch|  
|BULK INSERT|KEEPIDENTITY|引數|  
|INSERT ...SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|資料表提示|  
  
 如需詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)、[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)、[OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)、[INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)、[SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql) 和[資料表提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)。  
  
> [!NOTE]  
>  若要建立可用於多個資料表中或可在不參考任何資料表的情況下從應用程式進行呼叫的自動遞增數字，請參閱 [序號](../sequence-numbers/sequence-numbers.md)。  
  
## <a name="examples"></a>範例  
 本主題中的範例會使用 INSERT 來大量匯入資料 .。。SELECT * FROM OPENROWSET （BULK ...）並保留預設值。  
  
### <a name="sample-table"></a>範例資料表  
 大量匯入資料的範例需要在 **dbo** 結構描述下的 **AdventureWorks** 範例資料庫中，建立一個名為 **myTestKeepNulls** 的資料表。 建立這個資料表。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks;  
GO  
SELECT * INTO HumanResources.myDepartment   
   FROM HumanResources.Department  
      WHERE 1=0;  
GO  
SELECT * FROM HumanResources.myDepartment;  
```  
  
 `myDepartment` 所依據的 **Department** 資料表已將 IDENTITY_INSERT 設為 OFF。 因此，若要將資料匯入至識別欄位，您必須指定 KEEPIDENTITY 或 **-E**。  
  
### <a name="sample-data-file"></a>範例資料檔  
 大量匯入範例中所使用的資料檔包含從 `HumanResources.Department` 資料表中大量匯出的原生格式資料。 若要建立資料檔，請在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示字元中，輸入：  
  
```  
bcp AdventureWorks.HumanResources.Department out myDepartment-n.Dat -n -T  
```  
  
### <a name="sample-format-file"></a>範例格式檔案  
 大量匯入範例使用 XML 格式檔案 `myDepartment-f-x-n.Xml`，而它是使用原生資料格式。 這個範例使用 `bcp` 從 `HumanResources.Department` 資料庫的 `AdventureWorks` 資料表來產生這個格式檔案。 請在 Windows 命令提示字元之下，輸入：  
  
```  
bcp AdventureWorks.HumanResources.Department format nul -n -x -f myDepartment-f-n-x.Xml -T  
```  
  
 如需建立格式檔案的詳細資訊，請參閱[建立格式檔案 &#40;SQL Server&#41;](create-a-format-file-sql-server.md)。  
  
### <a name="a-using-bcp-and-keeping-identity-values"></a>A. 使用 bcp 並保留識別值  
 下列範例示範如何在使用 `bcp` 大量匯入資料時保留識別值。 `bcp` 命令會使用格式檔案 `myDepartment-f-n-x.Xml`，並包含下列參數：  
  
|限定詞|描述|  
|----------------|-----------------|  
|**-E**|指定將資料檔案中的識別值用於識別欄位。|  
|**-T**|指定`bcp`公用程式使用信任連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來連接到。|  
  
 在 Windows 命令提示字元中，輸入：  
  
```  
bcp AdventureWorks.HumanResources.myDepartment in C:\myDepartment-n.Dat -f C:\myDepartment-f-n-x.Xml -E -T  
  
```  
  
### <a name="b-using-bulk-insert-and-keeping-identity-values"></a>B. 使用 BULK INSERT 並保留識別值  
 下列範例使用 BULK INSERT 將資料從 `myDepartment-c.Dat` 檔案大量匯入 `AdventureWorks.HumanResources.myDepartment` 資料表。 該陳述式使用 `myDepartment-f-n-x.Xml` 格式檔案，並包含 KEEPIDENTITY 選項，以確保資料檔案中的任何識別值都會保留下來。  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
BULK INSERT HumanResources.myDepartment  
   FROM 'C:\myDepartment-n.Dat'  
   WITH (  
      KEEPIDENTITY,  
      FORMATFILE='C:\myDepartment-f-n-x.Xml'  
   );  
GO  
SELECT * FROM HumanResources.myDepartment;  
  
```  
  
### <a name="c-using-openrowset-and-keeping-identity-values"></a>C. 使用 OPENROWSET 並保留識別值  
 下列範例使用 OPENROWSET 大量資料列集提供者將資料從 `myDepartment-c.Dat` 檔案大量匯入 `AdventureWorks.HumanResources.myDepartment` 資料表。 該陳述式使用 `myDepartment-f-n-x.Xml` 格式檔案，並包含 KEEPIDENTITY 提示，以確保資料檔中的任何識別值都會保留下來。  
  
 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
  
INSERT INTO HumanResources.myDepartment  
   with (KEEPIDENTITY)  
   (DepartmentID, Name, GroupName, ModifiedDate)  
   SELECT *  
      FROM  OPENROWSET(BULK 'C:\myDepartment-n.Dat',  
      FORMATFILE='C:\myDepartment-f-n-x.Xml') as t1;  
GO  
  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
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
  
1.  [指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [使用 bcp 指定資料檔的前置長度 &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [使用 bcp 時指定檔案儲存類型 &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [資料表提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
