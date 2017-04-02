---
title: "使用疏鬆資料行 | Microsoft Docs"
ms.custom: ""
ms.date: "03/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "疏鬆資料行, 已描述"
  - "NULL 資料行"
  - "疏鬆資料行"
ms.assetid: ea7ddb87-f50b-46b6-9f5a-acab222a2ede
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# 使用疏鬆資料行
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  疏鬆資料行為已最佳化儲存位置來保存 Null 值的一般資料行。 疏鬆資料行會減少 Null 值的空間需求，但要付出擷取非 Null 值的更多成本負擔。 當空間至少節省了百分之 20 到 40 時，請考慮使用疏鬆資料行。 疏鬆資料行和資料行集是使用 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 或 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 陳述式所定義。  
  
 疏鬆資料行可以搭配資料行集和篩選的索引使用：  
  
-   資料行集  
  
     INSERT、UPDATE 和 DELETE 陳述式可以依名稱參考疏鬆資料行。 但是，您也可以檢視及處理資料表中結合至單一 XML 資料行的所有疏鬆資料行。 這個資料行稱為資料行集。 如需資料行集的詳細資訊，請參閱[使用資料行集](../../relational-databases/tables/use-column-sets.md)。  
  
-   篩選的索引  
  
     由於疏鬆資料行有許多 Null 值的資料列，所以它們特別適用於篩選的索引。 疏鬆資料行上篩選的索引只能針對已填入值的資料列來建立索引， 這樣會建立更小且更有效率的索引。 如需詳細資訊，請參閱 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。  
  
 疏鬆資料行和篩選的索引會啟用應用程式 (如 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)])，以便利用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 來有效率地儲存及存取使用者定義的大量屬性。  
  
## 疏鬆資料行的屬性  
 疏鬆資料行具有下列特性：  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會使用資料行定義中的 SPARSE 關鍵字，最佳化該資料行中值的儲存方式。 因此，當資料表中任何資料列的資料行值是 NULL 時，這些值就不需要儲存位置。  
  
-   具有疏鬆資料行之資料表的目錄檢視與一般資料表相同。 sys.columns 目錄檢視包含資料表中每一個資料行的資料列，而且也包含資料行集 (如果有定義的話)。  
  
-   疏鬆資料行是儲存層而非邏輯資料表的屬性。 因此，SELECT…INTO 陳述式不會將疏鬆資料行屬性複製到新資料表中。  
  
-   COLUMNS_UPDATED 函數會傳回 **varbinary** 值，指示 DML 動作期間已更新所有資料行。 COLUMNS_UPDATED 函數傳回的位元如下：  
  
    -   當明確更新疏鬆資料行時，該疏鬆資料行的對應位元會設定為 1，而資料行集的位元也會設定為 1。  
  
    -   當明確更新資料行集時，此資料行集的位元會設定為 1，而該資料表中所有疏鬆資料行的位元也會設定為 1。  
  
    -   若為插入作業，所有位元都會設定為 1。  
  
     如需資料行集的詳細資訊，請參閱[使用資料行集](../../relational-databases/tables/use-column-sets.md)。  
  
 下列資料類型無法指定為 SPARSE：  
  
|||  
|-|-|  
|**地理位置**|**text**|  
|**幾何**|**timestamp**|  
|**image**|**使用者定義資料類型**|  
|**ntext**||  
  
## 資料類型預計節省的空間  
 相較於未標示為 SPARSE 之相同資料所需的空間，疏鬆資料行需要更多的儲存空間來儲存非 Null 值。 下表顯示每一個資料類型的空間使用。 **NULL 百分比**資料行指出資料必須有多少百分比為 NULL，空間的淨節省才會是百分之 40。  
  
 **固定長度資料類型**  
  
|資料類型|非疏鬆位元組|疏鬆位元組|NULL 百分比|  
|---------------|---------------------|------------------|---------------------|  
|**bit**|0.125|5|98%|  
|**tinyint**|1|5|86%|  
|**smallint**|2|6|76%|  
|**int**|4|8|64%|  
|**bigint**|8|12|52%|  
|**real**|4|8|64%|  
|**float**|8|12|52%|  
|**smallmoney**|4|8|64%|  
|**money**|8|12|52%|  
|**smalldatetime**|4|8|64%|  
|**datetime**|8|12|52%|  
|**uniqueidentifier**|16|20|43%|  
|**date**|3|7|69%|  
  
 **與有效位數相關的長度資料類型**  
  
|資料類型|非疏鬆位元組|疏鬆位元組|NULL 百分比|  
|---------------|---------------------|------------------|---------------------|  
|**datetime2(0)**|6|10|57%|  
|**datetime2(7)**|8|12|52%|  
|**time(0)**|3|7|69%|  
|**time(7)**|5|9|60%|  
|**datetimetoffset(0)**|8|12|52%|  
|**datetimetoffset (7)**|10|14|49%|  
|**decimal/numeric(1,s)**|5|9|60%|  
|**decimal/numeric(38,s)**|17|21|42%|  
|**vardecimal(p,s)**|使用 **decimal** 類型作為保守估計。|||  
  
 **與資料相關的長度資料類型**  
  
|資料類型|非疏鬆位元組|疏鬆位元組|NULL 百分比|  
|---------------|---------------------|------------------|---------------------|  
|**sql_variant**|隨著基礎資料類型而不同|||  
|**varchar** 或 **char**|2*|4*|60%|  
|**nvarchar** 或 **nchar**|2*|4*+|60%|  
|**varbinary** 或 **binary**|2*|4*|60%|  
|**xml**|2*|4*|60%|  
|**hierarchyid**|2*|4*|60%|  
  
 *長度等於該類型所包含之資料的平均值，加上 2 或 4 個位元組。  
  
## 疏鬆資料行之更新所需的記憶體中負擔  
 設計具有疏鬆資料行的資料表時，請記住，如果要更新資料列，則資料表中的每個非 Null 疏鬆資料行都需要額外 2 個位元組的負擔。 由於存在這項額外記憶體需求，因此當資料列大小總計 (包括這個記憶體負擔) 超過 8019，而且無法從資料列發送任何資料行時，更新可能會非預期地失敗並發生錯誤 576。  
  
 假設某個資料表具有 600 個 bigint 類型的疏鬆資料行。 如果共有 571 個非 Null 資料行，則磁碟的大小總計就是 571 * 12 = 6852 個位元組。 加入額外資料列負擔和疏鬆資料行標頭之後，這個大小會增加至大約 6895 個位元組。 此頁面仍然具有大約 1124 個位元組的可用磁碟。 這可能會讓您以為其他資料行都可順利更新。 不過，在更新期間，記憶體中存在額外負擔，也就是 2\*(非 Null 疏鬆資料行的數目)。 在此範例中，加入額外負擔 (2 \* 571 = 1142 個位元組) 會將磁碟的資料列大小增加至大約 8037 個位元組。 這個大小超過了允許的大小上限：8019 個位元組。 因為所有資料行都是固定長度資料類型，所以無法從資料列發送資料行。 因此，更新就會失敗並發生 576 錯誤。  
  
## 使用疏鬆資料行的限制  
 疏鬆資料行可具有任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，而且其行為就像其他任何資料行一樣，但是有下列限制：  
  
-   疏鬆資料行必須可為 Null，而且不能有 ROWGUIDCOL 或 IDENTITY 屬性。 疏鬆資料行不能是以下資料類型：**text****ntext****image****timestamp****geometry** 或 **geography** FILESTREAM 屬性。  
  
-   疏鬆資料行不能有預設值。  
  
-   疏鬆資料行無法繫結至規則。  
  
-   雖然計算資料行可以包含疏鬆資料行，但是計算資料行不能標示為 SPARSE。  
  
-   可在疏鬆資料行上定義資料遮罩，但不能在屬於資料行集的疏鬆資料行上定義資料遮罩。  
  
-   疏鬆資料行不能為叢集索引或唯一主索引鍵索引的一部分。 但是，定義於疏鬆資料行上的保存和非保存的計算資料行都可以是叢集索引鍵的一部分。  
  
-   疏鬆資料行不能當做叢集索引或堆積的資料分割索引鍵使用； 但是，疏鬆資料行可以當做非叢集索引的資料分割索引鍵使用。  
  
-   疏鬆資料行不能是使用者定義資料表類型的一部分，該類型會用於資料表變數和資料表值參數中。  
  
-   疏鬆資料行與資料壓縮不相容。 因此，您無法將疏鬆資料行加入至壓縮的資料表，也無法壓縮包含疏鬆資料行的任何資料表。  
  
-   將資料行從疏鬆變更為非疏鬆 (或相反) 需要變更資料行的儲存格式。 SQL Server Database Engine 會使用下列程序來達成這項變更：  
  
    1.  以新的儲存大小和格式，將新的資料行加入至資料表。  
  
    2.  針對資料表中的每個資料列，將儲存在舊資料行中的值更新並複製到新的資料行。  
  
    3.  從資料表結構描述中移除舊的資料行。  
  
    4.  重建資料表 (如果沒有叢集索引)，或重建叢集索引以回收舊資料行使用的空間。  
  
    > [!NOTE]  
    >  當資料列中的資料大小超過允許的資料列大小上限時，步驟 2 可能會失敗。 這個大小包括儲存在舊資料行中的資料大小以及儲存在新資料行中的更新資料大小。 對於不包含任何疏鬆資料行的資料表而言，這個限制為 8060 個位元組。對於包含疏鬆資料行的資料表而言，這個限制為 8018 個位元組。 即使所有適合的資料行都已經從資料列發送，還是可能會發生這項錯誤。  
  
-   當您將非疏鬆資料行變更為疏鬆資料行時，此疏鬆資料行將會耗用更多的空間來儲存非 Null 值。 當資料列很接近資料列大小的上限時，此作業可能會失敗。  
  
## 支援疏鬆資料行的 SQL Server 技術  
 本章節說明下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術如何支援疏鬆資料行：  
  
-   異動複寫  
  
     異動複寫支援疏鬆資料行，但是不支援資料行集，資料行集可搭配疏鬆資料行使用。 如需資料行集的詳細資訊，請參閱[使用資料行集](../../relational-databases/tables/use-column-sets.md)。  
  
     SPARSE 屬性的複寫是由使用 [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中 [發行項屬性] 對話方塊所指定的結構描述選項所決定。 舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援疏鬆資料行。 如果您必須將資料複寫到舊版，請指定不應該複寫 SPARSE 屬性。  
  
     如果是發行的資料表，您不能將任何新的疏鬆資料行加入資料表，或是變更現有資料行的疏鬆屬性。 如果需要進行這類作業，請卸除發行集再重新建立。  
  
-   合併式複寫  
  
     合併式複寫不支援疏鬆資料行或資料行集。  
  
-   變更追蹤  
  
     變更追蹤可支援疏鬆資料行和資料行集。 在資料表中更新資料行集時，變更追蹤會將此動作視為整個資料列的更新。 不會提供任何詳細的變更追蹤來取得透過資料行集更新作業所更新的明確疏鬆資料行集合。 如果透過 DML 陳述式明確更新疏鬆資料行，其上的變更追蹤將會正常運作，而且可以識別明確的已變更資料行集合。  
  
-   異動資料擷取  
  
     異動資料擷取可支援疏鬆資料行，但是不支援資料行集。  
  
-   複製資料表時，不會保留資料行的疏鬆屬性。  
  
## 範例  
 在此範例中，文件資料表包含常用的一組 `DocID` 和 `Title` 資料行。 生產小組想要所有生產文件的 `ProductionSpecification` 和 `ProductionLocation` 資料行。 行銷小組想要行銷文件的 `MarketingSurveyGroup` 資料行。 此範例的程式碼會建立一個使用疏鬆資料行的資料表，並將兩個資料列插入資料表中，然後選取資料表中的資料。  
  
> [!NOTE]  
>  此資料表只有五個資料行，以方便顯示及閱讀。 如果設定了 ANSI_NULL_DFLT_ON 選項，則將疏鬆資料行宣告為可為 Null 是選擇性的作業。  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE DocumentStore  
    (DocID int PRIMARY KEY,  
     Title varchar(200) NOT NULL,  
     ProductionSpecification varchar(20) SPARSE NULL,  
     ProductionLocation smallint SPARSE NULL,  
     MarketingSurveyGroup varchar(20) SPARSE NULL ) ;  
GO  
  
INSERT DocumentStore(DocID, Title, ProductionSpecification, ProductionLocation)  
VALUES (1, 'Tire Spec 1', 'AXZZ217', 27);  
GO  
  
INSERT DocumentStore(DocID, Title, MarketingSurveyGroup)  
VALUES (2, 'Survey 2142', 'Men 25 - 35');  
GO  
```  
  
 從資料表中選取所有資料行將會傳回一般的結果集。  
  
```  
SELECT * FROM DocumentStore ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID  Title        ProductionSpecification  ProductionLocation  MarketingSurveyGroup`  
  
 `1      Tire Spec 1  AXZZ217                  27                  NULL`  
  
 `2      Survey 2142  NULL                     NULL                Men 25-35`  
  
 由於生產部門對於行銷資料不感興趣，而且他們想要使用一個只會傳回感興趣之資料行的資料行清單，如下列查詢所示。  
  
```  
SELECT DocID, Title, ProductionSpecification, ProductionLocation   
FROM DocumentStore   
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID  Title        ProductionSpecification  ProductionLocation`  
  
 `1      Tire Spec 1  AXZZ217                  27`  
  
## 另請參閱  
 [使用資料行集](../../relational-databases/tables/use-column-sets.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  