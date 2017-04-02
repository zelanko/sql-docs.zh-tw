---
title: "載入 XML 資料 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XML 資料 [SQL Server], 載入"
  - "載入 XML 資料"
ms.assetid: d1741e8d-f44e-49ec-9f14-10208b5468a7
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 載入 XML 資料
  您可以透過幾種方式將 XML 資料傳送到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 例如：  
  
-   如果您將資料放在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的 [n]text 或 image 資料行中，則可使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 將資料表匯入更新的版本。 使用 ALTER TABLE 陳述式將資料行類型變更為 XML。  
  
-   您可以使用 bcp out 從其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫大量複製資料，然後再使用 bcp in 將資料大量插入更新版本的資料庫。  
  
-   如果您將資料放在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的關聯式資料行中，請建立一個含有 [n]text 資料行的新資料表，並可選擇加入主索引鍵資料行來放置資料列識別碼。 使用用戶端程式設計來擷取在伺服器上以 FOR XML 產生的 XML，並將它寫入 **[n]text** 資料行。 然後使用先前提到的技巧，將資料傳送至更新版本的資料庫。 您可以選擇直接將 XML 寫入更新版本資料庫中的 XML 資料行。  
  
## 大量載入 XML 資料  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的大量載入功能 (例如 bcp) 來將 XML 資料大量載入伺服器中。 OPENROWSET 可讓您將資料從檔案載入至 XML 資料行中。 下列範例將說明這一點。  
  
##### 範例：從檔案載入 XML  
 此範例顯示如何在資料表 T 中插入資料列。XML 資料行的值從檔案 C:\MyFile\xmlfile.xml 載入成 CLOB，並且在整數資料行中提供值 10。  
  
```  
INSERT INTO T  
SELECT 10, xCol  
FROM    (SELECT *      
    FROM OPENROWSET (BULK 'C:\MyFile\xmlfile.xml', SINGLE_CLOB)   
 AS xCol) AS R(xCol)  
```  
  
## 文字編碼方式  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以 Unicode (UTF-16) 來儲存 XML 資料。 從伺服器擷取出來的 XML 資料會成為 UTF-16 編碼。 如果您要使用不同的編碼，則必須對所擷取的資料執行必要的轉碼作業。 有時 XML 資料可能會使用不同的編碼。 若有這種情形，您在載入資料時要特別小心。 例如：  
  
-   如果您的文字 XML 是 Unicode (UCS-2、UTF-16) 編碼，則可將它指派至 XML 資料行、變數或參數，都不會有任何問題。  
  
-   如果因為來源字碼頁的關係，編碼不是 Unicode 而且是隱含的，則資料庫中的字串字碼頁應與您要載入的字碼指標相同或相容。 若有必要，請使用 COLLATE。 如果沒有這類的伺服器字碼頁存在，則必須加入含有正確編碼的明確 XML 宣告。  
  
-   若要使用明確的編碼，請使用 **varbinary()** 類型 (與字碼頁沒有互動) 或使用適當字碼頁的字串類型。 然後再將資料指派給 XML 資料行、變數或參數。  
  
### 範例：明確地指定編碼方式  
 假設您將 XML 文件 vcdoc 儲存成沒有明確 XML 宣告的 **varchar(max)**。 下列陳述式會加入具有編碼 "iso8859-1" 的 XML 宣告、串連 XML 文件、將結果轉換成 **varbinary(max)**，位元組表示法因而保存下來，最後再轉換成 XML。 這樣可以讓 XML 處理器依據所指定的編碼 "iso8859-1" 來剖析資料，並針對字串值來產生對應的 UTF-16 表示法。  
  
```  
SELECT CAST(   
CAST (('<?xml version="1.0" encoding="iso8859-1"?>'+ vcdoc) AS VARBINARY (MAX))   
 AS XML)  
```  
  
### 字串編碼不相容  
 若您將 XML 複製並以字串常值形式貼到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [查詢編輯器] 視窗中，就可能會造成 [N]VARCHAR 字串編碼不相容。 這取決於 XML 執行個體的編碼而定。 在許多情況下，您可能會想要移除 XML 宣告。 例如：  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
  <xsd:schema …  
```  
  
 接著您應該加入 N，使 XML 執行個體成為 Unicode 執行個體。 例如：  
  
```  
-- Assign XML instance to a variable.  
DECLARE @X XML  
SET @X = N'…'  
-- Insert XML instance into an xml type column.  
INSERT INTO T VALUES (N'…')  
-- Create an XML schema collection  
CREATE XML SCHEMA COLLECTION XMLCOLL1 AS N'<xsd:schema … '  
```  
  
## 另請參閱  
 [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  