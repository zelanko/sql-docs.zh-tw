---
title: 使用 SQL 陳述式中的項目 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: caf8f68221c1ac14649bf10be0105e1e691c7482
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129961"
---
# <a name="elements-used-in-sql-statements"></a>SQL 陳述式中使用的項目
先前所列的 SQL 陳述式中，會使用下列項目。  
  
## <a name="element"></a>項目  
 *base-table-identifier* ::= *user-defined-name*  
  
 *base-table-name* ::= *base-table-identifier*  
  
 *布林值因數*:: = [NOT]*布林值-主要*  
  
 *boolean-primary* ::= comparison *-predicate* &#124; ( *search-condition* )  
  
 *布林值字詞*:: =*布林因數*[AND*布林詞彙*]  
  
 *character-string-literal* ::= ''{*character*}...'' (*字元*是驅動程式/資料來源之字元集中的任何字元。 若要包含單引號的常值字元 （"） 字元的字串常值中，使用兩個常值的引號字元 ['']。)  
  
 *資料行識別碼*:: =*使用者定義名稱*  
  
 *資料行名稱*:: = [*資料表名稱*。]*資料行識別碼*  
  
 *comparison-operator* ::= < &#124; > &#124; \<= &#124; >= &#124; = &#124; <>  
  
 *比較述詞*:: =*運算式*比較運算子運算式  
  
 *資料型別*:: =*字元字串型別*(*字元字串類型*是""DATA_TYPE""中的資料行 SQLGetTypeInfo 傳回的結果集的任一個 SQL_CHAR 任何資料型別或SQL_VARCHAR。)  
  
 *digit* ::= 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *dynamic-parameter* ::= ?  
  
 *expression* ::= term &#124; expression {+&#124;-} term  
  
 *factor* ::= [ *+* &#124; *-* ]*primary*  
  
 *insert-value* ::=  
  
 *dynamic-parameter*  
  
 &#124;*常值*  
  
 &#124; NULL  
  
 &#124; USER  
  
 *字母*:: =*大小 case 字母&#124;上限大小寫字母*  
  
 *literal* ::= *character-string-literal*  
  
 *大小 case 字母*:: = &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; i &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r&#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *order by 子句*:: = ORDER BY*排序規格*[，*排序規格*]...  
  
 *主要*:: =*資料行名稱*  
  
 &#124; *dynamic-parameter*  
  
 &#124;*常值*  
  
 &#124; ( *expression* )  
  
 *搜尋條件*:: =*布林值字詞*[或者*搜尋條件*]  
  
 *select 清單*:: = \* &#124; *子清單的 select* [，*選取子清單*]... (*select 清單*不能包含參數。)  
  
 *select-sublist* ::= *expression*  
  
 *排序規格*:: = {*不帶正負號整數&#124;資料行名稱*} [*ASC &#124; DESC*]  
  
 *table-identifier* ::= *user-defined-name*  
  
 *table-name* ::= *table-identifier*  
  
 *table-reference* ::= *table-name*  
  
 *table-reference-list* ::= *table-reference* [,*table-reference*]...  
  
 *term* ::= *factor* &#124; *term* {\*&#124; */* } *factor*  
  
 *不帶正負號整數*:: = {*數字*}  
  
 *大小寫字母大寫*:: =*的&#124;B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H&#124;我&#124;J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; &#124;Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *user-defined-name* ::= *letter*[*digit* &#124; *letter* &#124; *_* ]...
