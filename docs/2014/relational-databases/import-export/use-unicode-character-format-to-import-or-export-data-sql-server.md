---
title: 使用 Unicode 字元格式匯入或匯出資料 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34e8f4a5b49c9e023c224e62c23326864ef26f65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011644"
---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>使用 Unicode 字元格式匯入或匯出資料 (SQL Server)
  使用含有擴充/DBCS 字元的資料檔在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間大量傳送資料時，建議使用 Unicode 字元格式。 Unicode 字元資料格式可允許從伺服器匯出資料時所使用的字碼頁，與執行作業之用戶端所使用的字碼頁不同。 在此情況下，使用 Unicode 字元格式具有下列優點：  
  
-   如果來源資料和目的地資料都是 Unicode 資料類型，使用 Unicode 字元格式可保留所有的字元資料。  
  
-   如果來源資料和目的地資料不是 Unicode 資料類型，使用 Unicode 字元格式可使來源資料中，擴充字元的遺失可能性降到最低 (該擴充字元無法在目的地中表示)。  
  
 Unicode 字元格式資料檔遵循 Unicode 檔案的慣例。 檔案的前兩個位元組是十六進位數字 0xFFFE。 這些位元組可作為位元組順序的遮罩，指定先儲存或後儲存高順序的位元組至檔案中。  
  
> [!IMPORTANT]  
>  如果格式檔案要與 Unicode 字元資料檔案搭配使用，則所有的輸入欄位都必須是 Unicode 文字字串 (也就是固定大小或以字元結束的 Unicode 字串)。  
  
 儲存在 Unicode 字元格式資料檔的 `sql_variant` 資料，其操作方式和在字元格式資料檔中相同，不同之處在於資料是儲存為 `nchar`，而非 `char` 資料。 如需詳細資訊，請參閱 [定序和 Unicode 支援](../collations/collation-and-unicode-support.md)。  
  
 若要使用 Unicode 字元格式預設值以外的欄位或資料列結束字元，請參閱[指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)。  
  
## <a name="command-options-for-unicode-character-format"></a>Unicode 字元格式的命令選項  
 您可以使用 **bcp**、BULK INSERT 或 INSERT 等選項，將 Unicode 字元格式資料匯入資料表。SELECT \* FROM OPENROWSET(BULK...)。若是 **bcp** 命令或 BULK INSERT 陳述式，您可以在命令列上指定資料格式。 針對 INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式，您必須在格式檔案中指定資料格式。  
  
 下列命令列選項支援 Unicode 字元格式：  
  
|命令|選項|描述|  
|-------------|------------|-----------------|  
|**bcp**|**-w**|使用 Unicode 字元格式。|  
|BULK INSERT|DATAFILETYPE **='** widechar **'**|大量匯入資料時，使用 Unicode 字元格式。|  
  
 如需詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)、[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  或者，您可以在格式檔案中按照每個欄位指定格式。 如需詳細資訊，請參閱 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)＞。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用 **bcp** 大量匯出 Unicode 字元資料，以及如何使用 BULK INSERT 大量匯入相同的資料。  
  
### <a name="sample-table"></a>範例資料表  
 下列範例會要求在 `myTestUniCharData` 結構描述底下的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫中建立一個名為 `dbo` 的資料表。 您必須先建立這個資料表，才能執行範例。 若要建立這個資料表，請在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestUniCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 若要擴展這個資料表及檢視產生的內容，請執行下列陳述式：  
  
```  
INSERT INTO myTestUniCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3')   
        ,(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
  
```  
  
### <a name="using-bcp-to-bulk-export-unicode-character-data"></a>使用 bcp 大量匯出 Unicode 字元資料  
 若要從資料表將資料匯出到資料檔案，請使用 **bcp** 配合 **out** 選項與下列限定詞：  
  
|限定詞|描述|  
|----------------|-----------------|  
|**-w**|指定 Unicode 字元格式。|  
|**-t** `,`|指定逗號 (`,`) 作為欄位結束字元。<br /><br /> 注意:預設欄位結束字元是 tab 鍵 Unicode 字元 (\t)。 如需詳細資訊，請參閱 [指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)。|  
|**-T**|指定 **bcp** 公用程式使用整合式安全性的信任連接，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T**，則必須指定 **-U** 與 **-P**，才能順利登入。|  
  
 下列範例會將 Unicode 字元格式的資料，從 `myTestUniCharData` 資料表大量匯出到名為 `myTestUniCharData-w.Dat` 的新資料檔，並使用逗號 (`,`) 做為欄位結束字元。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示字元中，輸入：  
  
```  
bcp AdventureWorks2012..myTestUniCharData out C:\myTestUniCharData-w.Dat -w -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-unicode-character-data"></a>使用 BULK INSERT 大量匯入 Unicode 字元資料  
 下列範例會使用 `BULK INSERT`，將 `myTestUniCharData-w.Dat` 資料檔中的資料匯入至 `myTestUniCharData` 資料表。 您必須在陳述式中宣告非預設的欄位結束字元 (`,`)。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestUniCharData   
   FROM 'C:\myTestUniCharData-w.Dat'   
   WITH (  
      DATAFILETYPE='widechar',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [定序和 Unicode 支援](../collations/collation-and-unicode-support.md)  
  
  
