---
title: "自主資料庫定序 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- contained database, collations
ms.assetid: 4b44f6b9-2359-452f-8bb1-5520f2528483
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 777ff52e5670d97b6dfe3813d8e05dfcccf00103
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="contained-database-collations"></a>自主資料庫定序
  許多屬性會影響文字資料的排序次序和相等語意，包括區分大小寫、區分腔調字和使用的基底語言。 這些品質會透過資料的定序選擇表達至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需定序本身的更深入討論，請參閱[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
 定序不只會套用至儲存在使用者資料表中的資料，還會套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所處理的所有文字，包括中繼資料、暫存物件、變數名稱等。在自主及非自主資料庫中，這些項目的處理方式有所不同。 雖然這項變更不會影響許多使用者，不過有助於提供執行個體獨立性和統一性。 但是，這項變更可能也會導致一些混淆，並且導致同時存取包含和非自主資料庫的工作階段發生問題。  
  
 本主題將釐清此變更的內容，並且檢查此變更可能會導致問題的區域。  
  
## <a name="non-contained-databases"></a>非自主資料庫  
 所有資料庫都具有預設定序 (可在建立或改變資料庫時設定)。 這個定序會用於資料庫中的所有中繼資料，以及資料庫中所有字串資料行的預設值。 使用者可以使用 **COLLATE** 子句，針對任何特定的資料行選擇不同的定序。  
  
### <a name="example-1"></a>範例 1  
 例如，如果我們在北京工作，可能會使用中文定序：  
  
```tsql  
ALTER DATABASE MyDB COLLATE Chinese_Simplified_Pinyin_100_CI_AS;  
```  
  
 現在，如果我們建立一個資料行，其預設定序就是這個中文定序，但是如果我們想要，也可以選擇另一個定序：  
  
```tsql  
CREATE TABLE MyTable  
      (mycolumn1 nvarchar,  
      mycolumn2 nvarchar COLLATE Frisian_100_CS_AS);  
GO  
SELECT name, collation_name  
FROM sys.columns  
WHERE name LIKE 'mycolumn%' ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```tsql  
name            collation_name  
--------------- ----------------------------------  
mycolumn1       Chinese_Simplified_Pinyin_100_CI_AS  
mycolumn2       Frisian_100_CS_AS  
```  
  
 這段程式碼似乎相當簡單，不過卻引發許多問題。 因為資料行的定序相依於建立資料表所在的資料庫，所以使用儲存在 **tempdb**中的暫存資料表就會引發問題。 **tempdb** 的定序通常符合執行個體的定序，但不需要符合資料庫定序。  
  
### <a name="example-2"></a>範例 2  
 例如，假設上述 (中文) 資料庫使用於具有 **Latin1_General** 定序的執行個體上：  
  
```tsql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max)) ;  
GO  
```  
  
 第一眼看起來，這兩個資料表看似具有相同的結構描述，不過因為資料庫的定序不同，所以其值實際上不相容：  
  
```  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 訊息 468，層級 16，狀態 9，行 2  
  
 無法解析 equal to 作業中 "Latin1_General_100_CI_AS_KS_WS_SC" 及 "Chinese_Simplified_Pinyin_100_CI_AS" 之間的定序衝突。  
  
 修正此問題的方法是明確地建立暫時資料表的定序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可提供 **COLLATE** 子句的 **DATABASE_DEFAULT** 關鍵字，以簡化此作業。  
  
```tsql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max) COLLATE DATABASE_DEFAULT);  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 這段程式碼現在執行時不會發生錯誤。  
  
 我們也可以使用變數來查看定序相依的行為。 以下列函數為例：  
  
```  
CREATE FUNCTION f(@x INT) RETURNS INT  
AS BEGIN   
      DECLARE @I INT = 1  
      DECLARE @İ INT = 2  
      RETURN @x * @i  
END;  
```  
  
 這是相當罕見的函數。 在區分大小寫的定序中，Return 子句中的 @i 無法繫結至 @I 或 @İ。 在不區分大小寫的 Latin1_General 定序中，@i 會繫結至 @I，而且函數會傳回 1。 但是，在不區分大小寫的土耳其文定序中，@i 會繫結至 @İ，而且函數會傳回 2。 這在具有不同定序之執行個體之間移動的資料庫上可能會造成破壞。  
  
## <a name="contained-databases"></a>自主資料庫  
 因為自主資料庫的設計目標是要讓它們各自獨立，所以必須切斷執行個體和 **tempdb** 定序的相依性。 為了達到此目的，自主資料庫導入了目錄定序的概念。 目錄定序會用於系統中繼資料和暫時性物件。 下面將提供詳細資料。  
  
 在自主資料庫中，目錄定序 **Latin1_General_100_CI_AS_WS_KS_SC**。 對於所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上之所有自主資料庫而言，這個定序都相同，而且無法變更。  
  
 雖然資料庫定序會保留下來，不過只當做使用者資料的預設定序使用。 資料庫定序預設會等於模型資料庫定序，但是使用者可透過 **CREATE** 或 **ALTER DATABASE** 命令加以變更，就如同非自主資料庫一樣。  
  
 **COLLATE**子句提供了新的關鍵字 **CATALOG_DEFAULT** 。 在包含和非自主資料庫中，這個關鍵字會當做中繼資料之目前定序的捷徑使用。 也就是說，在非自主資料庫中， **CATALOG_DEFAULT** 將傳回目前資料庫定序，因為中繼資料已在資料庫定序中定序。 在自主資料庫中，這兩個值可能會不同，因為使用者可以變更資料庫定序，讓它不符合目錄定序。  
  
 下表將摘要說明包含和非自主資料庫中各種物件的行為：  
  
||||  
|-|-|-|  
|**項目**|**非自主資料庫**|**自主資料庫**|  
|使用者資料 (預設值)|COLLATE|COLLATE|  
|暫存資料 (預設值)|TempDB 定序|COLLATE|  
|中繼資料|DATABASE_DEFAULT / CATALOG_DEFAULT|COLLATE|  
|暫存中繼資料|TempDB 定序|COLLATE|  
|變數|執行個體定序|COLLATE|  
|Goto 標籤|執行個體定序|COLLATE|  
|資料指標名稱|執行個體定序|COLLATE|  
  
 在先前所描述的暫存資料表範例中，我們可以看見這個定序行為排除了在大部分暫存資料表中使用明確 **COLLATE** 子句的需求。 在自主資料庫中，這段程式碼現在執行時不會發生錯誤，即使資料庫和執行個體定序不同也一樣：  
  
```tsql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max));  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 這段程式碼會正常運作，因為 `T1_txt` 和 `T2_txt` 已在自主資料庫的資料庫定序中定序。  
  
## <a name="crossing-between-contained-and-uncontained-contexts"></a>跨越包含與未包含的內容  
 只要自主資料庫中的工作階段維持包含狀態，它就必須保留在所連接的資料庫中。 在此情況下，其行為非常直接。 但是，如果工作階段跨越包含與非包含的內容，其行為就會變得更複雜，因為您必須橋接這兩組規則。 部分自主資料庫可能會發生這種情況，因為使用者可能會針對另一個資料庫執行 **USE** 。 在此情況下，定序規則的差異是由下列原則處理。  
  
-   批次的定序行為是由批次開始的資料庫所決定。  
  
 請注意，這項決定是在發出任何命令之前進行，包括初始 **USE**。 也就是說，如果批次在自主資料庫中開始，但是第一個命令是針對非自主資料庫執行 **USE** ，包含的定序行為仍然會用於該批次。 根據這點，變數的參考可能會產生多個可能的結果：  
  
-   參考可能只會尋找一個符合項目。 在此情況下，參考運作時不會發生錯誤。  
  
-   參考可能不會在先前存在符合項目的目前定序中尋找符合項目。 這會引發錯誤，表示變數不存在，即使顯然已建立變數也一樣。  
  
-   參考可能會尋找原本不同的多個相符項目。 這也會引發錯誤。  
  
 我們將使用一些範例來說明這點。 在這些範例中，我們假設有一個名為 `MyCDB` 之部分自主資料庫，而且其資料庫定序設定為預設定序 **Latin1_General_100_CI_AS_WS_KS_SC**。 此外，我們假設執行個體定序為 **Latin1_General_100_CS_AS_WS_KS_SC**。 這兩個定序只有區分大小寫不同。  
  
### <a name="example-1"></a>範例 1  
 下列範例將說明參考只會尋找一個符合項目的案例。  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #a VALUES(1);  
GO  
  
USE master;  
GO  
  
SELECT * FROM #a;  
GO  
  
Results:  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
x  
-----------  
1  
```  
  
 在此情況下，識別的 #a 會在不區分大小寫的目錄定序與區分大小寫的執行個體定序中繫結，而且程式碼正常運作。  
  
### <a name="example-2"></a>範例 2  
 下列範例將說明參考不會在先前存在符合項目的目前定序中尋找符合項目的案例。  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #A VALUES(1);  
GO  
```  
  
 此處，#A 會繫結至不區分大小寫之預設定序中的 #a，而且插入作業正常運作。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
```  
  
 但是，如果我們繼續執行指令碼...  
  
```  
USE master;  
GO  
  
SELECT * FROM #A;  
GO  
```  
  
 當我們嘗試繫結至區分大小寫之執行個體定序中的 #A 時，就會收到錯誤。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 訊息 208，層級 16，狀態 0，行 2  
  
 無效的物件名稱 '#A'。  
  
### <a name="example-3"></a>範例 3  
 下列範例將說明參考會尋找原本不同的多個相符項目的案例。 首先，我們會在 **tempdb** (與執行個體具有相同的區分大小寫定序) 中啟動，然後執行下列陳述式。  
  
```  
USE tempdb;  
GO  
  
CREATE TABLE #a(x int);  
GO  
CREATE TABLE #A(x int);  
GO  
INSERT INTO #a VALUES(1);  
GO  
INSERT INTO #A VALUES(2);  
GO  
```  
  
 這個陳述式會成功執行，因為在此定序中，這些資料表各不相同：  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
(1 row(s) affected)  
```  
  
 不過，如果我們移入自主資料庫，就會發現無法再繫結至這些資料表。  
  
```  
USE MyCDB;  
GO  
SELECT * FROM #a;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 訊息 12800，層級 16，狀態 1，行 2  
  
 暫存資料表名稱 '#a' 的參考模稜兩可，無法解析。 可能的候選方式為 '#a' 和 '#A'。  
  
## <a name="conclusion"></a>結論  
 自主資料庫的定序行為與非自主資料庫稍有不同。 這種行為通常很有用，可提供執行個體獨立性和簡單性。 但是，某些使用者可能會遇到問題，尤其是當工作階段同時存取包含和非自主資料庫時。  
  
## <a name="see-also"></a>另請參閱  
 [自主資料庫](../../relational-databases/databases/contained-databases.md)  
  
  
