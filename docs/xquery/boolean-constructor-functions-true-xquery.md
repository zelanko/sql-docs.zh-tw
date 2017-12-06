---
title: "true 函數 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f38cd50748b59b2a0cf32e5a7e9ab0a28f7e396b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="boolean-constructor-functions---true-xquery"></a>布林建構函式為 true (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 xs:boolean 值 True。 這相當於 `xs:boolean("1")`。  
  
## <a name="syntax"></a>語法  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型 AdventureWorks 資料庫中的資料行。  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>A. 使用 true() XQuery 布林函數  
 下列範例會查詢不具型別的**xml**變數。 中的運算式**value （)**方法會傳回布林值**true （)**如果"aaa"是屬性的值。 **Value （)**方法**xml**資料類型轉換成位元的布林值，並傳回它。  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 在下列範例中，指定的查詢是針對具類型**xml**資料行。 `if` 運算式會檢查 <`ROOT`> 元素的具類型布林值，並據此傳回建構的 XML。 本範例將執行下列動作：  
  
-   建立 XML 結構描述集合，在其中定義 xs:boolean 類型的 <`ROOT`> 元素。  
  
-   建立含有具類型的資料表**xml**使用 XML 結構描述集合的資料行。  
  
-   將 XML 執行個體儲存在資料行中，並查詢它。  
  
```  
-- Drop table if exist  
--DROP TABLE T  
--go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="ROOT" type="boolean" nillable="true"/>  
</schema>'  
go  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<ROOT xmlns="QNameXSD">true</ROOT>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare namespace a="QNameXSD";   
   if (/a:ROOT[1] eq true()) then  
       <result>Found boolean true</result>  
   else  
       <result>Found boolean false</result>')  
  
FROM T  
-- result = <result>Found boolean true</result>  
-- Clean up  
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
```  
  
## <a name="see-also"></a>請參閱  
 [布林建構函式 &#40;XQuery &#41;](http://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)  
  
  
