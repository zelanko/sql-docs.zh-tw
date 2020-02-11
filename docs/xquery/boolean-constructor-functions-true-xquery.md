---
title: true 函數（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
author: rothja
ms.author: jroth
ms.openlocfilehash: 56f2dde1899340f036024253405379e094de59a6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039040"
---
# <a name="boolean-constructor-functions---true-xquery"></a>布林建構函式 - true (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 xs:boolean 值 True。 這相當於 `xs:boolean("1")`。  
  
## <a name="syntax"></a>語法  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中。  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>A. 使用 true() XQuery 布林函數  
 下列範例會查詢不具類型的**xml**變數。 如果 "aaa" 是屬性值， **value （）** 方法中的運算式會傳回布林值**true （）** 。 **Xml**資料類型的**value （）** 方法會將布林值轉換成位，並傳回它。  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 在下列範例中，查詢是針對具類型的**xml**資料行所指定。 `if`運算式會檢查 <`ROOT`> 元素的具類型布林值，並據以傳回已建立的 XML。 本範例將執行下列動作：  
  
-   建立 XML 架構集合，以定義 xs： `ROOT` boolean 類型的 <> 元素。  
  
-   使用 XML 架構集合，建立具有具類型**xml**資料行的資料表。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [&#40;XQuery&#41;的布林函式函數](https://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)  
  
  
