---
title: 使用 Unicode 原生格式匯入或匯出資料 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- Unicode [SQL Server], bulk importing and exporting
- data formats [SQL Server], Unicode native
ms.assetid: a6213308-f3d5-406e-9029-19d8bb3367f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b1d115dacc53cb074080931c2ebad88dcaf1c68d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011570"
---
# <a name="use-unicode-native-format-to-import-or-export-data-sql-server"></a>使用 Unicode 原生格式匯入或匯出資料 (SQL Server)
  當必須從某個[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝將資訊複製到另一個時，Unicode 原生格式會很有説明。 對非字元的資料使用原生格式可節省時間，消除在資料類型與字元格式之間，不必要的來回轉換。 對所有字元資料使用 Unicode 字元格式，可以防止在使用不同字碼頁的伺服器之間大量傳送資料期間，失去任何擴充字元。 任何大量匯入方法都可以讀取以 Unicode 原生格式表示的資料檔。  
  
 建議使用 Unicode 原生格式，在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間，使用包含擴充字元或 DBCS 字元的資料檔，大量傳送資料。 若是非字元資料，Unicode 原生格式會使用原生 (資料庫) 資料類型。 若是字元資料，如 `char`、`nchar`、`varchar`、`nvarchar`、`text`、`varchar(max)`、`nvarchar(max)` 及 `ntext`，Unicode 原生格式會使用 Unicode 字元資料格式。  
  
 以 SQLVARIANT 儲存在 Unicode 原生格式資料檔的 `sql_variant` 資料，會以它在原生格式資料檔的相同方式操作，不同處是 `char` 及 `varchar` 值會轉換為 `nchar` 及 `nvarchar`，這會讓受影響資料行所需的儲存體數量加倍。 原始中繼資料會加以保留，而且在大量匯入資料表資料行時，這些值會轉換回它們的原始 `char` 及 `varchar` 資料類型。  
  
## <a name="command-options-for-unicode-native-format"></a>Unicode 原生格式的命令選項  
 您可以使用**bcp**、BULK INSERT 或 INSERT ...，將 Unicode 原生格式資料匯入資料表中。SELECT \* FROM OPENROWSET （BULK ...）。對於**bcp**命令或 BULK INSERT 語句，您可以在命令列上指定資料格式。 對於 INSERT...SELECT * FROM OPENROWSET(BULK...) 陳述式，您必須在格式檔案中指定資料格式。  
  
 下列選項支援 Unicode 原生格式：  
  
|Command|選項|描述|  
|-------------|------------|-----------------|  
|**in**|**-N**|使**bcp**公用程式使用 Unicode 原生格式，其會針對所有的字元（`char`、 `nchar`、 `varchar` `nvarchar` `text`、、和`ntext`）資料使用原生（資料庫）資料類型做為所有的非字元資料和 unicode 字元資料格式。|  
|BULK INSERT|DATAFILETYPE **= '** widenative **'**|當大量匯入資料時，使用 Unicode 原生格式。|  
  
 如需詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)、[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  或者，您可以在格式檔案中按照每個欄位指定格式。 如需詳細資訊，請參閱 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)＞。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用 **bcp** 大量匯出原生資料，以及使用 BULK INSERT 大量匯入相同的資料。  
  
### <a name="sample-table"></a>範例資料表  
 以上範例需要在 **dbo** 結構描述下的 **AdventureWorks** 範例資料庫中，建立一個名為 **myTestUniNativeData** 的資料表。 您必須先建立這個資料表，才能執行範例。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestUniNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 若要擴展這個資料表及檢視產生的內容，請執行下列陳述式：  
  
```  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>使用 bcp 大量匯出原生資料  
 若要從資料表將資料匯出到資料檔案，請使用 **bcp** 配合 **out** 選項與下列限定詞：  
  
|限定詞|描述|  
|----------------|-----------------|  
|**-N**|指定原生資料類型。|  
|**-T**|指定 **bcp** 公用程式使用整合式安全性的信任連接，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，則必須指定 **-U** 與 **-P** ，才能順利登入。|  
  
 下列範例會以原生格式從 `myTestUniNativeData` 資料表，將資料大量匯出至名為 `myTestUniNativeData-N.Dat` 資料檔的新資料檔。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示字元中，輸入：  
  
```  
bcp AdventureWorks..myTestUniNativeData out C:\myTestUniNativeData-N.Dat -N -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>使用 BULK INSERT 大量匯入原生資料  
 下列範例使用 BULK INSERT 將 `myTestUniNativeData-N.Dat` 資料檔中的資料匯入至 `myTestUniNativeData` 資料表。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestUniNativeData   
    FROM 'C:\myTestUniNativeData-N.Dat'   
   WITH (DATAFILETYPE='widenative');   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
