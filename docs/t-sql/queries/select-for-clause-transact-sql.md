---
title: "FOR 子句 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FOR
- FOR CLAUSE
- FOR_TSQL
- FOR_CLAUSE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- XML option [SQL Server]
- BROWSE option
- FOR clause [Transact-SQL]
ms.assetid: 08a6f084-8f73-4f2a-bae4-3c7513dc99b9
caps.latest.revision: "54"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 51924cf8a6715e8966911b33c4c1cf691326322c
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="select---for-clause-transact-sql"></a>選取-FOR 子句 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  您可以使用 FOR 子句來指定查詢結果的下列選項的其中一個。  
  
-   允許在瀏覽模式資料指標中檢視查詢結果，藉由指定更新**FOR BROWSE**。  
  
-   查詢結果格式化為 XML，藉由指定**FOR XML**。  
  
-   指定查詢結果格式化為 JSON **FOR JSON**。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
[ FOR { BROWSE | <XML> | <JSON>} ]  
  
<XML> ::=  
XML   
{   
    { RAW [ ( 'ElementName' ) ] | AUTO }   
    [   
        <CommonDirectivesForXML>   
        [ , { XMLDATA | XMLSCHEMA [ ( 'TargetNameSpaceURI' ) ] } ]   
        [ , ELEMENTS [ XSINIL | ABSENT ]   
    ]  
  | EXPLICIT   
    [   
        <CommonDirectivesForXML>   
        [ , XMLDATA ]   
    ]  
  | PATH [ ( 'ElementName' ) ]   
    [  
        <CommonDirectivesForXML>   
        [ , ELEMENTS [ XSINIL | ABSENT ] ]  
    ]  
}   
  
<CommonDirectivesForXML> ::=   
[ , BINARY BASE64 ]  
[ , TYPE ]  
[ , ROOT [ ( 'RootName' ) ] ]  
  
<JSON> ::=  
JSON   
{   
    { AUTO | PATH }   
    [   
        [ , ROOT [ ( 'RootName' ) ] ]  
        [ , INCLUDE_NULL_VALUES ]  
        [ , WITHOUT_ARRAY_WRAPPER ]  
    ]  
  
}  
```  
  
## <a name="for-browse"></a>FOR BROWSE  
 BROWSE  
 指定允許在檢視 DB-Library 瀏覽模式資料指標中的資料時進行更新。 資料表可瀏覽應用程式中如果資料表包括**時間戳記**資料行，資料表具有唯一的索引，且 FOR BROWSE 選項的執行個體傳送的 SELECT 陳述式結尾[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  您無法使用\<lock_hint > HOLDLOCK 包含 FOR BROWSE 選項的 SELECT 陳述式中。
  
 FOR BROWSE 不能出現在 UNION 運算子所聯集的 SELECT 陳述式中。  
  
> [!NOTE]  
>  當資料表的唯一索引鍵資料行可設為 Null 時，資料表是在外部聯結的內側，瀏覽模式並不支援索引。  
  
 此瀏覽模式可讓您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中掃描資料列，並且更新資料表中的資料 (一次一個資料列)。 若要存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表應用程式瀏覽模式中，您必須使用下列兩個選項的其中一個：  
  
-   您用來存取資料的 SELECT 陳述式您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表必須以關鍵字結尾**FOR BROWSE**。 當您開啟**FOR BROWSE**選項以便使用瀏覽模式中，建立暫存資料表。  
  
-   您必須執行下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式來使用瀏覽模式開啟**NO_BROWSETABLE**選項：  
  
    ```  
    SET NO_BROWSETABLE ON  
    ```  
  
     當您開啟**NO_BROWSETABLE**選項時，所有 SELECT 陳述式的行為如同**FOR BROWSE**選項已附加至陳述式。 不過， **NO_BROWSETABLE**選項不會建立暫存資料表， **FOR BROWSE**選項通常用來將結果傳送給您的應用程式。  
  
 當您嘗試存取的資料從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的資料表使用瀏覽模式的 SELECT 查詢，包含外部聯結陳述式，並已針對存在外部聯結陳述式內部資料表上定義唯一索引時，瀏覽模式不會不 sup連接埠的唯一索引。 只有當所有唯一索引的索引鍵資料行都可以接受 Null 值時，瀏覽模式才會支援此唯一索引。 如果下列條件成立，瀏覽模式就不支援此唯一索引：  
  
-   您嘗試存取的資料從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表中的瀏覽模式使用包含外部聯結陳述式的 SELECT 查詢。  
  
-   已針對存在外部聯結陳述式內部的資料表定義唯一索引。  
  
 若要在瀏覽模式中重新產生此行為，請遵循下列步驟：  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，建立名為 SampleDB 的資料庫。  
  
2.  在 SampleDB 資料庫中，建立同時包含名為 c1 之單一資料行的 tleft 資料表和 tright 資料表。 針對 tleft 資料表中的 c1 資料行定義唯一索引鍵，並且將此資料行設定為接受 Null 值。 若要這樣做，請在適當的查詢視窗中執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    CREATE TABLE tleft(c1 INT NULL UNIQUE) ;  
    GO   
    CREATE TABLE tright(c1 INT NULL) ;  
    GO  
    ```  
  
3.  在 tleft 資料表和 tright 資料表中插入多個值。 請確定您在 tleft 資料表中插入一個 Null 值。 若要這樣做，請在查詢視窗中執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    INSERT INTO tleft VALUES(2) ;  
    INSERT INTO tleft VALUES(NULL) ;  
    INSERT INTO tright VALUES(1) ;  
    INSERT INTO tright VALUES(3) ;  
    INSERT INTO tright VALUES(NULL) ;  
    GO  
    ```  
  
4.  開啟**NO_BROWSETABLE**選項。 若要這樣做，請在查詢視窗中執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    SET NO_BROWSETABLE ON ;  
    GO  
    ```  
  
5.  透過在 SELECT 查詢中使用外部聯結陳述式，存取 tleft 資料表和 tright 資料表中的資料。 請確定 tleft 資料表位於外部聯結陳述式的內部。 若要這樣做，請在查詢視窗中執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    SELECT tleft.c1   
    FROM tleft   
    RIGHT JOIN tright   
    ON tleft.c1 = tright.c1   
    WHERE tright.c1 <> 2 ;  
  
    ```  
  
     請在結果窗格中注意下列輸出：  
  
     c1  
  
     ---\-  
  
     NULL  
  
     NULL  
  
 在您以瀏覽模式執行 SELECT 查詢來存取資料表之後，由於右方外部聯結陳述式的定義，所以 SELECT 查詢的結果集就會針對 tleft 資料表中的 c1 資料行包含兩個 Null 值。 因此，在結果集中，您無法區別來自此資料表的 Null 值與右方外部聯結陳述式所導入的 Null 值。 如果您必須忽略結果集的 Null 值，可能會收到不正確的結果。  
  
> [!NOTE]  
>  如果唯一索引中包含的資料行不接受 Null 值，表示結果集中的所有 Null 值都是由右方外部聯結陳述式所導入。  
  
## <a name="for-xml"></a>FOR XML  
 XML  
 指定查詢結果要以 XML 文件來傳回。 您必須指定下列 XML 模式之一：RAW、AUTO、EXPLICIT。 如需有關 XML 資料和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱[FOR XML &#40;SQL Server &#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
 原始 [ **('***ElementName***')** ]  
 使用查詢結果，並將結果集的泛用識別碼的 XML 項目每個資料列轉換\<資料列 / > 作為元素標記。 您可以選擇性地指定資料列元素的名稱。 所產生的 XML 輸出利用指定*ElementName*作為產生每個資料列的資料列元素。 如需詳細資訊，請參閱[搭配 FOR XML 使用 RAW 模式](../../relational-databases/xml/use-raw-mode-with-for-xml.md)和[搭配 FOR XML 使用 RAW 模式](../../relational-databases/xml/use-raw-mode-with-for-xml.md)。  
  
 AUTO  
 將查詢結果以簡易巢狀 XML 樹狀結構傳回。 在 SELECT 子句中至少列出一個資料行的 FROM 子句中的每份資料表，都會表示成一個 XML 元素。 列在 SELECT 子句中的資料行會對應到適當的元素屬性。 如需詳細資訊，請參閱 [搭配 FOR XML 使用 AUTO 模式](../../relational-databases/xml/use-auto-mode-with-for-xml.md)。  
  
 EXPLICIT  
 指定產生之 XML 樹狀結構的形狀已明確地定義。 當使用這個模式時，必須依照特定方式來撰寫查詢，以便明確指定所需巢狀結構的其他相關資訊。 如需詳細資訊，請參閱 [搭配 FOR XML 使用 EXPLICIT 模式](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)。  
  
 XMLDATA  
 傳回內嵌 XDR 結構描述，但不在結果中加入根元素。 如果指定了 XMLDATA，就會將 XDR 結構描述附加至文件中。  
  
> [!IMPORTANT]  
>  XMLDATA 指示詞已被取代。 在 RAW 和 AUTO 模式的情況下，請使用 XSD 產生。 EXPLICIT 模式中沒有 XMLDATA 指示詞的替代項目。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 XMLSCHEMA [ **('***TargetNameSpaceURI***')** ]  
 傳回內嵌 XSD 結構描述。 您可以在指定這個指示詞時，選擇性地指定目標命名空間 URI，這會在結構描述中傳回指定的命名空間。 如需詳細資訊，請參閱 [產生內嵌 XSD 結構描述](../../relational-databases/xml/generate-an-inline-xsd-schema.md)。  
  
 ELEMENTS  
 指定以子元素來傳回資料行。 否則這些資料行會對應到 XML 屬性。 只有 RAW、AUTO 和 PATH 模式支援這個選項。 如需詳細資訊，請參閱 [搭配 FOR XML 使用 RAW 模式](../../relational-databases/xml/use-raw-mode-with-for-xml.md)。  
  
 XSINIL  
 指定的項目**xsi: nil**屬性設為**True**為 NULL 資料行值建立。 這個選項只能搭配 ELEMENTS 指示詞來指定。 如需詳細資訊，請參閱[使用 XSINIL 參數為 NULL 值產生的項目](../../relational-databases/xml/generate-elements-for-null-values-with-the-xsinil-parameter.md)。  
  
 ABSENT  
 指出對於 NULL 資料行值而言，不會在 XML 結果中加入對應的 XML 元素。 請只搭配 ELEMENTS 來指定這個選項。  
  
 路徑 [ **('***ElementName***')** ]  
 會產生\<資料列 > 元素包裝函數的結果集中的每個資料列。 您可以選擇性地指定的元素名稱\<資料列 > 元素包裝函數。 如果提供空字串，例如 FOR XML PATH (**'**))，則不會產生包裝函數元素。 使用 PATH 可能會針對利用 EXPLICIT 指示詞來撰寫的查詢提供較簡單的替代方案。 如需詳細資訊，請參閱 [搭配 FOR XML 使用 PATH 模式](../../relational-databases/xml/use-path-mode-with-for-xml.md)。  
  
 BINARY BASE64  
 指定查詢用二進位 Base64 編碼格式來傳回二進位資料。 當您利用 RAW 和 EXPLICIT 模式來擷取二進位資料時，您必須指定這個選項。 這是 AUTO 模式的預設值。  
  
 TYPE  
 指定查詢會傳回結果為**xml**型別。 如需詳細資訊，請參閱 [FOR XML 查詢中的 TYPE 指示詞](../../relational-databases/xml/type-directive-in-for-xml-queries.md)。  
  
 ROOT [ **('***RootName***')** ]  
 指定將單一最上層元素加入產生的 XML 中。 您可以選擇性地指定要產生的根元素名稱。 如果未指定選擇性的根名稱，預設值\<根目錄 > 加入項目。  
  
 如需詳細資訊，請參閱[FOR XML &#40;SQL Server &#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
 **XML 範例**  
  
 下列範例指定設定了 `FOR XML AUTO` 和 `TYPE` 選項的 `XMLSCHEMA`。 因為`TYPE`選項時，結果集傳回給用戶端**xml**型別。 `XMLSCHEMA` 選項指定將內嵌 XSD 結構描述包括在傳回的 XML 資料中，`ELEMENTS` 選項指定 XML 結果以元素為中心。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT p.BusinessEntityID, FirstName, LastName, PhoneNumber AS Phone  
FROM Person.Person AS p  
JOIN Person.PersonPhone AS pph ON p.BusinessEntityID  = pph.BusinessEntityID  
WHERE LastName LIKE 'G%'  
ORDER BY LastName, FirstName   
FOR XML AUTO, TYPE, XMLSCHEMA, ELEMENTS XSINIL;  
```  
  
## <a name="for-json"></a>FOR JSON  
 JSON  
 指定 FOR JSON，將傳回的查詢結果格式化為 JSON 文字。 您也必須指定下列 JSON 模式之一： 自動或路徑。 如需有關**FOR JSON**子句，請參閱[查詢結果格式化為 JSON 與 FOR JSON &#40;SQL Server &#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 AUTO  
 格式的 JSON 輸出會自動根據的結構**選取**陳述式  
            藉由指定**FOR JSON AUTO**。 如需詳細資訊和範例，請參閱[使用 AUTO 模式自動格式化 JSON 輸出 &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)。  
  
 PATH  
 藉由指定取得的 JSON 輸出格式的完整控制權   
            **FOR JSON PATH**。 **PATH** 模式讓您建立包裝函式物件和巢狀複雜屬性。 如需詳細資訊和範例，請參閱[以 PATH 模式格式化巢狀的 JSON 輸出 &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)。  
  
 INCLUDE_NULL_VALUES  
 在 JSON 輸出中包含 null 值，藉由指定**INCLUDE_NULL_VALUES**選項與**FOR JSON**子句。 如果您未指定此選項，輸出不會在查詢結果中包含 null 值的 JSON 屬性。 如需詳細資訊和範例，請參閱[使用 INCLUDE_NULL_VALUES 選項 &#40; JSON 輸出中包含 Null 值SQL Server &#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).  
  
 ROOT [ **('***RootName***')** ]  
 指定將單一最上層元素新增至 JSON 輸出**根**選項與**FOR JSON**子句。 如果您未指定 **ROOT** 選項，則 JSON 輸出不會有根項目。 如需詳細資訊和範例，請參閱[新增根節點與根選項 &#40; JSON 輸出SQL Server &#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
 WITHOUT_ARRAY_WRAPPER  
 移除來指定預設括住的 JSON 輸出的方括弧**WITHOUT_ARRAY_WRAPPER**選項與**FOR JSON**子句。 如果您未指定此選項，JSON 輸出以方括號括住。 使用**WITHOUT_ARRAY_WRAPPER**選項，以產生單一 JSON 物件做為輸出。  如需詳細資訊，請參閱 [使用 WITHOUT_ARRAY_WRAPPER 選項從 JSON 輸出移除方括弧 &#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md)。  
  
 如需詳細資訊，請參閱[使用 FOR JSON 將查詢結果格式化為 JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
