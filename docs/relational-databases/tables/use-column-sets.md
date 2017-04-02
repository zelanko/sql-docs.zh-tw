---
title: "使用資料行集 | Microsoft Docs"
ms.custom: ""
ms.date: "07/30/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "疏鬆資料行, 資料行集"
  - "資料行集"
ms.assetid: a4f9de95-dc8f-4ad8-b957-137e32bfa500
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# 使用資料行集
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  使用疏鬆資料行的資料表可以指定資料行集，以傳回資料表中的所有疏鬆資料行。 資料行集是不具類型的 XML 表示，可將資料表的所有疏鬆資料行結合到結構化輸出中。 資料行集類似於計算資料行，因為資料行集並未實際儲存在資料表中。 資料行集與計算資料行不同的地方在於資料行集可直接更新。  
  
 當資料表中的資料行數目很大，而且個別操作資料行很麻煩時，您應該考慮使用資料行集。 當應用程式在擁有許多資料行的資料表上使用資料行集來選取及插入資料時，可能會看到一些效能上的改善。 但是，當資料表中的資料行上定義許多索引時，資料行集的效能可能會降低。 這是因為執行計畫所需的記憶體數量增加的緣故。  
  
 若要定義資料行集，請在 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 或 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 陳述式中使用 *\<資料行集名稱>* FOR ALL_SPARSE_COLUMNS 關鍵字。  
  
## 使用資料行集的指導方針  
 使用資料行集時，請考慮下列指導方針：  
  
-   可以在相同的陳述式中加入疏鬆資料行和資料行集。  
  
-   如果資料表已包含疏鬆資料行，資料行集無法加入該資料表中。  
  
-   資料行集無法變更。 若要變更資料行集，您必須先刪除再重新建立疏鬆資料行和資料行集。  
  
-   如果資料表未包含任何疏鬆資料行，資料行集便可加入該資料表中。 如果之後將疏鬆資料行加入此資料表，這些資料行將會出現在資料行集中。  
  
-   一個資料表只能有一個資料行集。  
  
-   資料行集為選擇性，而且不必使用疏鬆資料行。  
  
-   資料行集上不能定義條件約束或預設值。  
  
-   計算資料行不能包含資料行集資料行。  
  
-   包含資料行集的資料表上不支援分散式查詢。  
  
-   複寫不支援資料行集。  
  
-   異動資料擷取不支援資料行集。  
  
-   資料行集不能是任何索引類型的一部分。 其中包括 XML 索引、全文檢索索引和索引檢視表。 資料行集不能當做任何索引中併入的資料行來加入。  
  
-   資料行集不能用於篩選索引的篩選運算式中或篩選的統計資料中。  
  
-   當檢視表包含資料行集時，此資料行集會當做 XML 資料行出現在檢視表中。  
  
-   資料行集不能併入索引檢視表定義中。  
  
-   當資料分割檢視依據名稱指定疏鬆資料行時，如果資料分割檢視包含了有包含資料行集的資料表，將可以進行更新。 如果資料分割檢視參考資料行集，將無法更新。  
  
-   不允許參考資料行集的查詢通知。  
  
-   XML 資料的大小限制為 2 GB。 如果資料列中所有非 null 疏鬆資料行的結合資料超出此限制，查詢或 DML 作業將會產生錯誤。  
  
-   如需 COLUMNS_UPDATED 函數傳回之資料的資訊，請參閱[使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)。  
  
## 從資料行集內選取資料的指導方針  
 當您從資料行集選取資料時，請考量以下的指導方針：  
  
-   在概念上，資料行集是一種可更新的 XML 計算資料行，可將一組基礎關聯式資料行彙總成單一 XML 表示。 此資料行集只支援 ALL_SPARSE_COLUMNS 屬性， 這個屬性是用來從特定資料列的所有疏鬆資料行中彙總所有非 null 值。  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 資料表編輯器中，資料行集會顯示為可編輯的 XML 欄位。 請使用以下格式定義資料行集：  
  
    ```  
    <column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...  
    ```  
  
     資料行集的值範例如下：  
  
    -   `<sparseProp1>10</sparseProp1><sparseProp3>20</sparseProp3>`  
  
    -   `<DocTitle>Bicycle Parts List</DocTitle><Region>West</Region>`  
  
-   資料行集的 XML 表示中會省略包含 null 值的疏鬆資料行。  
  
> [!WARNING]  
>  加入資料行集會變更 SELECT * 查詢的行為 此查詢會將資料行集當做 XML 資料行傳回，而且不會傳回個別的疏鬆資料行。 結構描述設計人員和軟體開發人員必須要小心，不能破壞現有的應用程式。  
  
## 在資料行集內插入或修改資料  
 若要執行疏鬆資料行的資料操作，可以使用個別資料行的名稱，或是參考資料行集的名稱，以及使用資料行集的 XML 格式來指定資料行集的值。 疏鬆資料行可依任何順序出現在 XML 資料行中。  
  
 當您使用 XML 資料行集來插入或更新疏鬆資料行值時，插入基礎疏鬆資料行內的值會從 **xml** 資料類型隱含地轉換。 如果是數值資料行，數值資料行之 XML 內的空白值會轉換成空白字串。 這樣會將零插入數值資料行中，如下列範例所示。  
  
```  
CREATE TABLE t (i int SPARSE, cs xml column_set FOR ALL_SPARSE_COLUMNS);  
GO  
INSERT t(cs) VALUES ('<i/>');  
GO  
SELECT i FROM t;  
GO  
```  
  
 在此範例中，`i` 資料行未指定任何值，但是插入了 `0` 的值。  
  
## 使用 sql_variant 資料類型  
 **sql_variant** 資料類型可以儲存多種不同的資料類型，例如 **int**、**char** 和 **date**。 資料行集會將與 **sql_variant** 值相關聯的資料類型資訊 (例如小數位數、有效位數和地區設定資訊)，輸出為產生之 XML 資料行內的屬性。 如果您嘗試在自訂產生的 XML 陳述式內提供這些屬性當做資料行集上插入或更新作業的輸入，某些屬性會是必要的，而且其中一些屬性會指派預設值。 下表列出當未提供值時，伺服器所產生的資料類型和預設值。  
  
|資料類型|localeID*|sqlCompareOptions|sqlCollationVersion|SqlSortId|最大長度|有效位數|小數位數|  
|---------------|----------------|-----------------------|-------------------------|---------------|--------------------|---------------|-----------|  
|**char**、**varchar**、**binary**|-1|'Default'|0|0|8000|不適用**|不適用|  
|**nvarchar**|-1|'Default'|0|0|4000|不適用|不適用|  
|**decimal**、**float**、**real**|不適用|不適用|不適用|不適用|不適用|18|0|  
|**integer**、**bigint**、**tinyint**、**smallint**|不適用|不適用|不適用|不適用|不適用|不適用|不適用|  
|**datetime2**|不適用|不適用|不適用|不適用|不適用|不適用|7|  
|**datetime offset**|不適用|不適用|不適用|不適用|不適用|不適用|7|  
|**datetime**、**date**、**smalldatetime**|不適用|不適用|不適用|不適用|不適用|不適用|不適用|  
|**money**、**smallmoney**|不適用|不適用|不適用|不適用|不適用|不適用|不適用|  
|**time**|不適用|不適用|不適用|不適用|不適用|不適用|7|  
  
 \*  localeID -1 表示預設地區設定。 英文地區設定是 1033。  
  
 **  不適用 = 在資料行集上的選取作業期間，沒有任何值是這些屬性的輸出。 當提供給插入或更新作業內資料行集的 XML 表示中的呼叫端指定這個屬性的值時，將會產生錯誤。  
  
## 安全性  
 資料行集之安全性模型的運作方式，類似於資料表和資料行之間存在的安全性模型。 資料行集可視為一個迷你資料表，而選取作業就像是此迷你資料表上的 SELECT * 作業。 但是，資料行集與疏鬆資料行之間的關聯性是一種群組關聯性，而不限為容器。 此安全性模型會檢查資料行集資料行上的安全性，並接受基礎疏鬆資料行上的 DENY 作業。 此安全性模型的其他特性如下：  
  
-   可以從資料行集資料行授與及撤銷安全性權限，類似於資料表中的任何其他資料行。  
  
-   資料行集資料行上 SELECT、INSERT、UPDATE、DELETE 和 REFERENCES 權限的 GRANT 或 REVOKE 不會傳播給該資料行集的基礎成員資料行。 它只適用於資料行集資料行的使用。 資料行集的 DENY 權限會傳播給資料表的基礎疏鬆資料行。  
  
-   在資料行集資料行上執行 SELECT、INSERT、UPDATE 和 DELETE 陳述式會要求使用者具有資料行集資料行的對應權限，同時具有資料表內所有疏鬆資料行的對應權限。 由於此資料行集表示資料表中的所有疏鬆資料行，所以您必須具有所有疏鬆資料行的權限，這包括您可能不要變更的疏鬆資料行。  
  
-   在疏鬆資料行或資料行集上執行 REVOKE 陳述式會將安全性預設為其父物件。  
  
## 範例  
 在下列範例中，文件資料表包含常用的一組 `DocID` 和 `Title` 資料行。 生產小組想要所有生產文件的 `ProductionSpecification` 和 `ProductionLocation` 資料行。 行銷小組想要行銷文件的 `MarketingSurveyGroup` 資料行。  
  
### A. 建立具有資料行集的資料表  
 下列範例會建立一個資料表，此資料表將使用疏鬆資料行，並包括資料行集 `SpecialPurposeColumns`。 此範例會將兩個資料列插入資料表中，然後選取資料表中的資料。  
  
> [!NOTE]  
>  此資料表只有五個資料行，以方便顯示及閱讀。  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE DocumentStoreWithColumnSet  
    (DocID int PRIMARY KEY,  
     Title varchar(200) NOT NULL,  
     ProductionSpecification varchar(20) SPARSE NULL,  
     ProductionLocation smallint SPARSE NULL,  
     MarketingSurveyGroup varchar(20) SPARSE NULL,  
     MarketingProgramID int SPARSE NULL,  
     SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS);  
GO  
```  
  
### B. 使用疏鬆資料行的名稱，將資料插入資料表中  
 下列範例會將兩個資料列插入範例 A 建立的資料表中。此範例會使用疏鬆資料行的名稱，而且不會參考資料行集。  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, ProductionSpecification, ProductionLocation)  
VALUES (1, 'Tire Spec 1', 'AXZZ217', 27);  
GO  
  
INSERT DocumentStoreWithColumnSet (DocID, Title, MarketingSurveyGroup)  
VALUES (2, 'Survey 2142', 'Men 25 - 35');  
GO  
```  
  
### C. 使用資料行集的名稱，將資料插入資料表中  
 下列範例會將第三個資料列插入範例 A 建立的資料表中。這次不會使用疏鬆資料行的名稱， 而是使用資料行集的名稱，而且插入作業會提供四個疏鬆資料行其中兩個的值 (使用 XML 格式)。  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, SpecialPurposeColumns)  
VALUES (3, 'Tire Spec 2', '<ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>');  
GO  
```  
  
### D. 在使用 SELECT * 時觀察資料行集的結果  
 以下範例會從包含資料行集的資料表中選取所有資料行， 它會傳回 XML 資料行，其中包含疏鬆資料行的結合值。 但是不會個別傳回疏鬆資料行。  
  
```  
SELECT DocID, Title, SpecialPurposeColumns FROM DocumentStoreWithColumnSet ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1      Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `2      Survey 2142  <MarketingSurveyGroup>Men 25 - 35</MarketingSurveyGroup>`  
  
 `3      Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### E. 觀察依據名稱選取資料行集的結果  
 由於生產部門對於行銷資料不感興趣，所以此範例加入 `WHERE` 子句來限制輸出。 此範例會使用資料行集的名稱。  
  
```  
SELECT DocID, Title, SpecialPurposeColumns  
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1     Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `3     Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### F. 觀察依據名稱選取疏鬆資料行的結果  
 當資料表包含資料行集時，您仍然可以使用個別資料行名稱來查詢此資料表，如下列範例所示。  
  
```  
SELECT DocID, Title, ProductionSpecification, ProductionLocation   
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        ProductionSpecification ProductionLocation`  
  
 `1     Tire Spec 1  AXZZ217                 27`  
  
 `3     Tire Spec 2  AXW9R411                38`  
  
### G. 使用資料行集更新資料表  
 下列範例會使用該資料列所用之兩個疏鬆資料行的新值來更新第三筆記錄。  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification><ProductionLocation>38</ProductionLocation>'  
WHERE DocID = 3 ;  
GO  
```  
  
> [!IMPORTANT]  
>  使用資料行集的 UPDATE 陳述式會更新資料表內的所有疏鬆資料行。 未參考的疏鬆資料行將會更新為 NULL。  
  
 下列範例會更新第三筆記錄，但是只會指定兩個已填入之資料行其中一個的值。 第二個資料行 `ProductionLocation` 不會併入 `UPDATE` 陳述式中，而且會更新為 NULL。  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification>'  
WHERE DocID = 3 ;  
GO  
```  
  
## 另請參閱  
 [使用疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md)  
  
  