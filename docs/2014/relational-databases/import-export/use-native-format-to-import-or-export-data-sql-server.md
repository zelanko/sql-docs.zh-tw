---
title: 使用原生格式匯入或匯出資料 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2e91899172dfc6d640df0c33c77e32de3c1c21c
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011655"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>使用原生格式匯入或匯出資料 (SQL Server)
  在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間，使用不包含任何擴充/雙位元組字集 (DBCS) 字元的資料檔傳送大量資料時，建議使用原生格式。  
  
> [!NOTE]  
>  若要在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間，使用包含擴充或 DBCS 字元的資料檔大量傳送資料，您應該使用 Unicode 原生格式。 如需詳細資訊，請參閱 [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)。  
  
 原生格式會維持資料庫的原生資料類型。 原生格式的目的是為了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表之間進行資料的高速資料傳送。 如果您使用格式檔案，則來源與目標資料表不需要相同。 資料傳送包含兩個步驟：  
  
1.  將來源資料表中的資料大量匯出到資料檔  
  
2.  將資料檔中的資料大量匯入目標資料表  
  
 在相同資料表之間使用原生格式，可避免資料類型與字元格式間進行不需要的來回轉換，因而可節省時間及空間。 不過，若要取得最佳的傳輸率，必須針對資料格式化做一些檢查。 若要防止所載入的資料發生問題，請參閱下列限制清單。  
  
## <a name="restrictions"></a>限制  
 若要以原生格式成功匯入資料，請確定：  
  
-   資料檔具有原生格式。  
  
-   目標資料表必須與資料檔相容 (具有正確的資料行數目、資料類型、長度、NULL 狀態等等)，否則您必須使用格式檔案，將每一個欄位對應到它的對應資料行。  
  
    > [!NOTE]  
    >  如果您從與目標資料表不相符的檔案匯入資料，匯入作業或許會成功，但是插入目標資料表的資料值可能不正確。 原因是檔案中的資料是使用目標資料表的格式來解譯。 因此，任何不相符都會導致插入的值不正確。 不過，這樣的不相符在任何情況下，都不會導致資料庫中發生邏輯或實體不一致性。  
  
     如需使用格式檔案的詳細資訊，請參閱[匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)。  
  
 成功的匯入作業不會損毀目標資料表。  
  
## <a name="how-bcp-handles-data-in-native-format"></a>bcp 如何處理原生格式的資料  
 本節討論 **bcp** 公用程式如何匯出及匯入原生格式資料的特殊考量。  
  
-   非字元資料  
  
     bcp 公用程式使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部二進位資料格式，將資料表中的非字元資料寫入資料檔。  
  
-   `char` 或 `varchar` 資料  
  
     每個開頭`char`或是`varchar`欄位中， **bcp**加入前置長度。  
  
    > [!IMPORTANT]  
    >  使用原生模式時，依預設，**bcp** 公用程式會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的字元轉換為 OEM 字元，然後再將它們複製到資料檔。 **bcp** 公用程式會將資料檔中的字元轉換為 ANSI 字元，然後再將它們大量匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 在進行這些轉換期間，可能會遺失擴充字元。 如有擴充字元，請使用 Unicode 原生格式或指定字碼頁。  
  
-   `sql_variant` 資料  
  
     如果 `sql_variant` 資料以原生格式資料檔儲存為 SQLVARIANT，則資料會維持它所有的特性。 用來記錄每一個資料值的資料類型的中繼資料，會與資料值一起儲存。 中繼資料是用來以目的地 `sql_variant` 資料行中相同的資料類型，重新建立資料值。  
  
     如果目的地資料行的資料類型不是 `sql_variant`，則每一個資料值將依照隱含資料轉換的一般規則，轉換為目的地資料行的資料類型。 如果資料轉換期間發生錯誤，將會回復目前批次。 任何在 `char` 資料行之間傳送的 `varchar` 及 `sql_variant` 值，都可能有字碼頁轉換問題。  
  
     如需資料轉換的詳細資訊，請參閱[資料類型轉換 &#40;Database Engine&#41;](/sql/t-sql/data-types/data-type-conversion-database-engine)。  
  
## <a name="command-options-for-native-format"></a>原生格式的命令選項  
 您可以將原生格式資料匯入資料表，方法是使用 **bcp**、BULK INSERT 或 INSERT ...SELECT \* FROM OPENROWSET(BULK...)。若是 **bcp** 命令或 BULK INSERT 陳述式，您可以在命令列上指定資料格式。 針對 INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式，您必須在格式檔案中指定資料格式。  
  
 下列命令列選項支援原生格式：  
  
|命令|選項|描述|  
|-------------|------------|-----------------|  
|**bcp**|**-n**|會導致**bcp**公用程式來使用原生資料類型的資料。<sup>1</sup>|  
|BULK INSERT|DATAFILETYPE **='** native **'**|使用資料的原生或 widenative 資料類型。 請注意，如果利用了格式檔案指定資料類型，就不需要 DATAFILETYPE。|  
  
 <sup>1</sup>載入原生 (**-n**) 與舊版相容的格式資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端，使用 **-V**切換。 如需詳細資訊，請參閱 [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)。  
  
 如需詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)、[BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) 或 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)。  
  
> [!NOTE]  
>  或者，您可以在格式檔案中按照每個欄位指定格式。 如需詳細資訊，請參閱 [匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)＞。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用 **bcp** 大量匯出原生資料，以及使用 BULK INSERT 大量匯入相同的資料。  
  
### <a name="sample-table"></a>範例資料表  
 這些範例需要在 **AdventureWorks** 範例資料庫中，以 **dbo** 結構描述建立一個名為 **myTestNativeData** 的資料表。 您必須先建立這個資料表，才能執行範例。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 若要擴展這個資料表及檢視產生的內容，請執行下列陳述式：  
  
```  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>使用 bcp 大量匯出原生資料  
 若要從資料表將資料匯出到資料檔案，請使用 **bcp** 配合 **out** 選項與下列限定詞：  
  
|限定詞|描述|  
|----------------|-----------------|  
|**-n**|指定原生資料類型。|  
|**-T**|指定 **bcp** 公用程式使用整合式安全性的信任連接，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果未指定 **-T** ，則必須指定 **-U** 與 **-P** ，才能順利登入。|  
  
 下列範例會以原生格式從 `myTestNativeData` 資料表，將資料大量匯出至名為 `myTestNativeData-n.Dat` 資料檔的新資料檔。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 命令提示字元中，輸入：  
  
```  
bcp AdventureWorks..myTestNativeData out C:\myTestNativeData-n.Dat -n -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>使用 BULK INSERT 大量匯入原生資料  
 下列範例使用 BULK INSERT 將 `myTestNativeData-n.Dat` 資料檔中的資料匯入至 `myTestNativeData` 資料表。 在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 查詢編輯器中，執行：  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestNativeData   
    FROM 'C:\myTestNativeData-n.Dat'   
   WITH (DATAFILETYPE='native');   
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [sql_variant &#40;Transact-SQL&#41;](/sql/t-sql/data-types/sql-variant-transact-sql)   
 [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
