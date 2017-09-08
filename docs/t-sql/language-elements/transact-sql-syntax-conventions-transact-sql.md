---
title: "TRANSACT-SQL 語法慣例 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql13.TSQLExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- conventions [SQL Server]
- Applies to section in Transact-SQL topics
- code example conventions [SQL Server]
- objects [SQL Server], names
- code [SQL Server], conventions
- multipart names [SQL Server]
- Transact-SQL syntax conventions
- syntax conventions [SQL Server]
- code [SQL Server]
- Transact-SQL
- naming conventions [SQL Server]
- syntax [SQL Server], Transact-SQL
ms.assetid: 35fbcf7f-8b55-46cd-a957-9b8c7b311241
caps.latest.revision: 55
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a1c60d865d1b18eae1cd89ea226e91e8e7b5b9e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="transact-sql-syntax-conventions-transact-sql"></a>TRANSACT-SQL 語法慣例 Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  下表列出和描述 [!INCLUDE[tsql](../../includes/tsql-md.md)] 參考中之語法圖所用的慣例。  
  
|慣例|用於|  
|----------------|--------------|  
|UPPERCASE|[!INCLUDE[tsql](../../includes/tsql-md.md)] 關鍵字。|  
|*斜體*|使用者提供的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法參數。|  
|**粗體字**|必須完全依照顯示來輸入的資料庫名稱、資料表名稱、資料行名稱、索引名稱、預存程序、公用程式、資料類型名稱和文字。|  
|**底線**|指出省略陳述式中包含附加底線之值的子句時，所套用的預設值。|  
|&#124; (分隔號)|加上括號或大括號來分隔語法項目。 您只可以選擇其中一個項目。|  
|`[ ]` (方括弧)|選擇性的語法項目。 不要鍵入方括號。|  
|{ } (大括號)|必要的語法項目。 不要鍵入大括號。|  
|[**,**...*n*]|指出先前項目可以重複 *n* 次。 以逗號分開各次出現項目。|  
|[...*n*]|指出先前項目可以重複 *n* 次。 以空白分開各次出現項目。|  
|;|[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式結束字元。雖然這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中的大部分陳述式都不需要使用分號，但是未來的版本可能會需要使用分號。|  
|\<標籤 >:: =|語法區塊的名稱。 這個慣例可用來分組與標示冗長語法的區段，或分組與標示可用於陳述式中之多個位置的語法單位。 在您可以使用語法區塊的每個位置 > 形箭號括住的標籤表示：\<標籤 >。<br /><br /> 一組是集合運算式，例如\<群組集合 >; 清單位於集合的集合，例如\<複合元素清單 >。|  
  
## <a name="multipart-names"></a>多部分名稱  
 除非另有指定，否則，所有指向資料庫物件名稱的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 參考都可以是四部分的名稱，格式如下：  
  
 *server_name* **。**[*database_name*]**。**[*schema_name*]**。***object_name*  
  
 | *database_name***。**[*schema_name*]**。***object_name*  
  
 | *schema_name***。***object_name*  
  
 *|object_name*  
  
 *伺服器名稱*  
 指定連結伺服器名稱或遠端伺服器名稱。  
  
 *database_name*  
 指定當物件在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機執行個體中之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的名稱。 連結的伺服器物件時*database_name*指定 OLE DB 目錄。  
  
 *schema_name*  
 指定如果物件是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中，包含物件的結構描述名稱。 連結的伺服器物件時*schema_name*指定 OLE DB 結構描述名稱。  
  
 *object_name*  
 指向物件名稱。  
  
 當參考特定物件時，您不一定需要指定伺服器、資料庫和結構描述供 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 識別物件。 不過，如果找不到物件，就會傳回錯誤。  
  
> [!NOTE]  
>  若要避免名稱解析錯誤，我們建議您每當指定結構描述範圍的物件時，都要指定結構描述名稱。  
  
 若要省略中繼節點，請利用句點來表示這些位置。 下表顯示物件名稱的有效格式。  
  
|物件參考格式|Description|  
|-----------------------------|-----------------|  
|*伺服器* **。** *資料庫* **。** *結構描述* **。** *物件*|四部分名稱。|  
|*伺服器* **。** *資料庫* **...** *物件*|省略結構描述名稱。|  
|*伺服器* **...** *結構描述* **。** *物件*|省略資料庫名稱。|  
|*伺服器* **...** *物件*|省略資料庫和結構描述名稱。|  
|*資料庫* **。** *結構描述* **。** *物件*|省略伺服器名稱。|  
|*資料庫* **...** *物件*|省略伺服器和結構描述名稱。|  
|*結構描述* **。** *物件*|省略伺服器和資料庫名稱。|  
|*物件*|省略伺服器、資料庫和結構描述名稱。|  
  
## <a name="code-example-conventions"></a>程式碼範例慣例  
 除非另有指示，否則 [!INCLUDE[tsql](../../includes/tsql-md.md)] 參考中所提供的範例都是利用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 及其下列選項的預設值來測試的：  
  
-   ANSI_NULLS  
  
-   ANSI_NULL_DFLT_ON  
  
-   ANSI_PADDING  
  
-   ANSI_WARNINGS  
  
-   CONCAT_NULL_YIELDS_NULL  
  
-   QUOTED_IDENTIFIER  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 參考中的大部分程式碼範例都已在執行排序順序會區分大小寫的伺服器中測試過。 測試伺服器通常都是執行 ANSI/ISO 1252 字碼頁。  
  
 許多程式碼範例以字母的 Unicode 字元字串常數的前置詞**N**。不含**N**前置詞，字串會轉換成資料庫的預設字碼頁。 這個預設字碼頁可能無法辨識特定字元。  
  
## <a name="applies-to-references"></a>「適用於」參考  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]參考包括與相關的主題[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]， [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]， [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]， [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，和[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]。 在每個主題頂端附近，會有一個區段適用於這項主題主旨的產品。 對於未列出的產品，表示該主題不適用於該產品。 例如，可用性群組於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 引進。 **建立可用性群組**主題指出它適用於**SQL Server (SQL Server 2012 到目前的版本)**因為不適用於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]， [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]，或[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 在某些情況下，某產品或許適用於一般主題主旨，但所有的引數卻都無法使用。 例如自主資料庫使用者於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 引進。 **CREATE USER**陳述式可用於任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產品，但是**WITH PASSWORD**語法無法用於較舊版本。 在此情況下，額外**適用於**區段插入適當的引數中的說明主題的主體。  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 參考 &#40;Database Engine&#41;](../../t-sql/transact-sql-reference-database-engine.md)  
  
  



