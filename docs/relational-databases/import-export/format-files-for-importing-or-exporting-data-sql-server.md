---
title: "匯入或匯出資料的格式檔案 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk exporting [SQL Server], format files
- bulk importing [SQL Server], format files
- format files [SQL Server]
ms.assetid: b7b97d68-4336-4091-aee4-1941fab568e3
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: d0e3abc1c4ae024257be18f3e3ad3ba5f5566457
ms.contentlocale: zh-tw
ms.lasthandoff: 10/04/2017

---
# <a name="format-files-for-importing-or-exporting-data-sql-server"></a>匯入或匯出資料的格式檔案 (SQL Server)
  當您將資料大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，或從資料表大量匯出資料時，可以使用「格式檔案」來儲存大量匯出或大量匯入資料所需的所有格式資訊。 這包含相對於該資料表之資料檔中各欄位的格式資訊。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援兩種類型的格式檔案：XML 格式檔案和非 XML 格式檔案。 非 XML 格式檔案和 XML 格式檔案都會將每個欄位的描述包含在資料檔中，而且 XML 格式檔案也包含對應資料表資料行的描述。 一般而言，XML 和非 XML 格式檔案可以互換使用， 但是，仍建議您在新的格式檔案中使用 XML 語法，因為 XML 比非 XML 格式檔案多了一些優點。 如需詳細資訊，請參閱 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)。  
  
  
##  <a name="Benefits"></a> 格式檔案的優點  
  
-   提供可用來寫入資料檔的彈性系統，幾乎不需要進行編輯，即可符合其他資料格式或從其他軟體中讀取資料檔。  
  
-   可讓您大量匯入資料，而不需要加入或刪除不需要的資料，或是重新排列資料檔中的現有資料。 當資料檔欄位與資料表資料行不相符時，格式檔案就會特別有用。  
  
##  <a name="ExamplesOfFFs"></a> 格式檔案的範例  
 下列範例顯示非 XML 格式檔案及 XML 格式檔案的配置。 這些格式檔案會對應到 `HumanResources.myTeam` 範例資料庫中的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料表。 這個資料表包含四個資料行：`EmployeeID`、`Name`、`Title` 和 `ModifiedDate`。  
  
> [!NOTE]  
>  如需此資料表及建立方式的相關資訊，請參閱 [HumanResources.myTeam 範例資料表 &#40;SQL Server&#41;](../../relational-databases/import-export/humanresources-myteam-sample-table-sql-server.md)。  
  
### <a name="a-using-a-non-xml-format-file"></a>A. 使用非 XML 格式檔案  
 下列非 XML 格式檔案使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的 `HumanResources.myTeam` 原生資料格式。 這個格式檔案是使用下列 `bcp` 命令所建立。  
  
```cmd 
bcp AdventureWorks.HumanResources.myTeam format nul -f myTeam.Fmt -n -T   
The contents of this format file are as follows: 9.0  
4  
1       SQLSMALLINT   0       2       ""   1     EmployeeID               ""  
2       SQLNCHAR      2       100     ""   2     Name                     SQL_Latin1_General_CP1_CI_AS  
3       SQLNCHAR      2       100     ""   3     Title                    SQL_Latin1_General_CP1_CI_AS  
4       SQLNCHAR      2       100     ""   4     Background               SQL_Latin1_General_CP1_CI_AS  
```  
  
 如需詳細資訊，請參閱 [非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)。  
  
  
### <a name="b-using-an-xml-format-file"></a>B. 使用 XML 格式檔案  
 下列 XML 格式檔案使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的 `HumanResources.myTeam` 原生資料格式。 這個格式檔案是使用下列 `bcp` 命令所建立。  
  
```cmd
bcp AdventureWorks.HumanResources.myTeam format nul -f myTeam.Xml -x -n -T   
```  
  
 格式檔案包含：  
  
```xml
 <?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="NativePrefix" LENGTH="1"/>  
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="NCharPrefix" PREFIX_LENGTH="2" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="EmployeeID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Name" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Title" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Background" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 如需詳細資訊，請參閱 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)。  
  
  
##  <a name="WhenFFrequired"></a> 何時需要格式檔案？  
 INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式永遠需要格式檔案。  
  
-   至於 **bcp** 或 BULK INSERT，在簡單的情況下，可以選擇是否使用格式檔案，但很少會需要。 不過，在複雜的大量匯入情況下，就經常需要格式檔案。  
  
 下列情況需要格式檔案：  
  
-   多個具有不同結構描述的資料表，使用同一個資料檔做為來源。  
  
-   資料檔的欄位數目和目標資料表的資料行數目不同；例如：  
  
    -   目標資料表至少有一個資料行，其中定義了預設值或允許 NULL。  
  
    -   使用者在資料表中的一或多個資料行上沒有 SELECT/INSERT 權限。  
  
    -   兩個以上具有不同結構描述的資料表，使用單一資料檔。  
  
-   資料檔與資料表的資料行順序不同。  
  
-   資料檔的資料行之間，有不同的終止字元或前置長度。  
  
> [!NOTE]  
>  在沒有格式檔案的情況下，如果 **bcp** 命令指定資料格式參數 (**-n**、 **-c**、 **-w**或 **-N**)，或 BULK INSERT 作業指定 DATAFILETYPE 選項，則會採用指定的資料格式來做為解譯資料檔欄位的預設方法。  
  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
-   [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
## <a name="see-also"></a>另請參閱  
 [非 XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [XML 格式檔案 &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)   
 [大量匯入或大量匯出的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)  
  
  

