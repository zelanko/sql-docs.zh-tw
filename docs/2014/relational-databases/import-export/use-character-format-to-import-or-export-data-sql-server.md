---
title: 使用字元格式匯入或匯出資料 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab658be26dc8ccbdd4e760d0b1bc835ace3b2c38
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011673"
---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>使用字元格式匯入或匯出資料 (SQL Server)
  若要將資料大量匯出到用於其他程式的文字檔，或是要從其他程式產生的文字檔大量匯入資料，建議您使用字元格式。  
  
> [!NOTE]  
>  如果您要在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間大量傳送資料，而資料檔包含 Unicode 字元資料，但不含任何擴充字元或 DBCS 字元，請使用 Unicode 字元格式。 如需詳細資訊，請參閱 [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)。  
  
 字元格式會在所有的資料行中使用字元資料格式。 當資料用於其他程式中，例如試算表，或當資料需要從其他資料庫供應商 (例如 Oracle) 複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，以字元格式來儲存資訊就很有用。  
  
## <a name="considerations-for-using-character-format"></a>使用字元格式的考量  
 使用字元格式時，請考慮下列事項：  
  
-   依預設，**bcp** 公用程式會以定位字元分隔字元資料欄位，並以新行字元來結束記錄。 如需如何指定其他結束字元的相關資訊，請參閱[指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)。  
  
-   依預設，在大量匯出或匯入字元模式資料之前，會執行下列轉換：  
  
    |大量作業的方向|轉換|  
    |---------------------------------|----------------|  
    |匯出|將資料轉換成字元表示法。 若有明確要求，則字元資料行中的資料會轉換成所要求的字碼頁。 若未指定字碼頁，則會使用用戶端電腦的 OEM 字碼頁來轉換字元資料。|  
    |匯入|視需要將字元資料轉換成原生表示法，並將字元資料由用戶端字碼頁轉譯成目標資料行的字碼頁。|  
  
-   若要避免在轉換期間遺失擴充字元，請使用 Unicode 字元格式，或指定字碼頁。  
  
-   所有儲存在字元格式檔案中的 `sql_variant` 資料，會在沒有中繼資料的情況下儲存。 每個資料值會根據隱含資料轉換的規則，轉換成 `char` 格式。 匯入至 `sql_variant` 資料行時，資料會以 `char` 格式匯入。 要匯入的資料行如果不是採用 `sql_variant` 資料類型，則會使用隱含轉換將資料從 `char` 轉換過來。 如需資料轉換的詳細資訊，請參閱[資料類型轉換 &#40;Database Engine&#41;](/sql/t-sql/data-types/data-type-conversion-database-engine)。  
  
-   **Bcp**公用程式匯出`money`有四個位數小數點之後、 但沒有任何數字分位符號，例如逗點分隔符號字元格式資料檔的值。 例如，`money` 資料行包含的值 1,234,567.123456，會採用 1234567.1235 的字元字串，大量匯出到資料檔。  
  
## <a name="command-options-for-character-format"></a>字元格式的命令選項  
 您可以將字元格式資料匯入資料表，方法是使用 **bcp**、BULK INSERT 或 INSERT ...SELECT \* FROM OPENROWSET(BULK...)。若是 **bcp** 命令或 BULK INSERT 陳述式，您可以在命令列上指定資料格式。 針對 INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式，您必須在格式檔案中指定資料格式。  
  
 下列命令列選項支援字元格式：  
  
|命令|選項|描述|  
|-------------|------------|-----------------|  
|**bcp**|**-c**|會導致**bcp**公用程式使用字元資料。<sup>1</sup>|  
|BULK INSERT|DATAFILETYPE **='char'**|於大量匯入資料時使用字元格式。|  
  
 <sup>1</sup>載入字元 (**-c**) 與舊版相容的格式資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端，使用 **-V**切換。 如需詳細資訊，請參閱 [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)。  
  
 如需詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)、[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  或者，您可以在格式檔案中按照每個欄位指定格式。 如需詳細資訊，請參閱 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)＞。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用 **bcp** 以大量匯出字元資料，以及如何使用 BULK INSERT 大量匯入相同的資料。  
  
### <a name="sample-table"></a>範例資料表  
 以上範例需要在 **dbo** 結構描述下的 **AdventureWorks** 範例資料庫中，建立一個名為 **myTestCharData** 的資料表。 您必須先建立這個資料表，才能執行範例。 若要建立此資料表，請在 SQL [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中執行：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 若要擴展這個資料表及檢視產生的內容，請執行下列陳述式：  
  
```  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData  
  
```  
  
### <a name="using-bcp-to-bulk-export-character-data"></a>使用 bcp 大量匯出字元資料  
 若要從資料表將資料匯出到資料檔案，請使用 **bcp** 配合 **out** 選項與下列限定詞：  
  
|限定詞|描述|  
|----------------|-----------------|  
|**-c**|指定字元格式。|  
|**-t** `,`|指定逗號 (`,`) 作為欄位結束字元。<br /><br /> 注意:預設欄位結束字元是定位字元 (\t)。 如需詳細資訊，請參閱 [指定欄位與資料列結束字元 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)。|  
|**-T**|指定 **bcp** 公用程式使用整合式安全性的信任連接，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，則必須指定 **-U** 與 **-P** ，才能順利登入。|  
  
 下列範例會將字元格式的資料，從 `myTestCharData` 資料表大量匯出至名為 `myTestCharData-c.Dat` 的新資料檔，並使用逗號 (,) 做為欄位結束字元。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示字元中，輸入：  
  
```  
bcp AdventureWorks..myTestCharData out C:\myTestCharData-c.Dat -c -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-character-data"></a>使用 BULK INSERT 大量匯入字元資料  
 下列範例使用 BULK INSERT 將 `myTestCharData-c.Dat` 資料檔中的資料匯入至 `myTestCharData` 資料表。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestCharData   
   FROM 'C:\myTestCharData-c.Dat'   
   WITH (  
      DATAFILETYPE='char',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  
