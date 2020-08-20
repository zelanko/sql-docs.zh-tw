---
description: SQL 陳述式中使用的項目
title: SQL 語句中使用的元素 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c24f5dd55530e38ea47ed9a2b846d549bb26d56
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456571"
---
# <a name="elements-used-in-sql-statements"></a>SQL 陳述式中使用的項目
下列元素用於先前所列的 SQL 語句。  
  
## <a name="element"></a>元素  
 *基底資料表-識別碼* ：： = *使用者定義的名稱*  
  
 *基表名稱* ：： = *基底資料表-識別碼*  
  
 *布林值因數* ：： = [NOT] *布林值-主要*  
  
 *布林-主要* ：： = 比較 *-* 述詞 &#124; ( *搜尋條件* )   
  
 *布林值* ：： = *布林因數* [和 *布林值詞彙*]  
  
 *字元-字串-literal* ：： = ' ' {*character*} ... ' '  (*字元* 是驅動程式/資料來源之字元集中的任何字元。 若要在字元字串常值中包含單一常值引號字元 ( ' ' ) ，請使用兩個常值引號字元 [' ' ' ']。 )   
  
 資料*行識別碼*：： =*使用者定義的名稱*  
  
 資料*行名稱*：： = [*資料表名稱*]。資料*行識別碼*  
  
 *比較-運算子* ：： = < &#124; > &#124; \<= &#124; > = &#124; = &#124; <>  
  
 *比較-* 述詞：： = *運算式* 比較-運算子運算式  
  
 *資料類型* ：： = *字元-字串類型* (字元- *字串類型* 是任何資料類型，而 SQLGetTypeInfo 所傳回之結果集中的 "" DATA_TYPE "" 資料行可能是 SQL_CHAR 或 SQL_VARCHAR。 )   
  
 *數位* ：： = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *動態參數* ：： =？  
  
 *expression* ：： = term &#124; 運算式 {+&#124;-} 詞彙  
  
 *因素* ：： = [ *+*&#124;*-* ]*主要*  
  
 *insert-value* ：： =  
  
 *動態參數*  
  
 &#124;*常*值  
  
 &#124; Null  
  
 &#124; 使用者  
  
 *字母*：： =*小寫字母 &#124; 大寫*字母  
  
 *literal* ：： =*字元-字串-常*值  
  
 *小寫字母* ：： = a &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; i &#124; j &#124; k &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *order by 子句* ：： = order by *排序規格* [， *排序規格*] .。。  
  
 *primary* ：： = 資料 *行名稱*  
  
 &#124; *動態參數*  
  
 &#124;*常*值  
  
 &#124; ( *運算式* )   
  
 *搜尋條件* ：： = *布林詞彙* [或 *搜尋條件*]  
  
 *select-list* ：： = \* &#124; *select-* 子清單 [， *select-子清單*] ... (*select 清單* 不能包含參數。 )   
  
 *select-子清單* ：： = *expression*  
  
 *排序規格* ：： = {不*帶正負號的整數 &#124; 資料行名稱*} [*ASC &#124; DESC*]  
  
 *資料表-識別碼* ：： = *使用者定義的名稱*  
  
 *資料表名稱* ：： = *資料表-識別碼*  
  
 *資料表參考* ：： = *資料表名稱*  
  
 *資料表參考清單* ：： = *資料表參考* [，*資料表參考*] .。。  
  
 *詞彙* ：： = *因素* &#124; *詞彙* { \*&#124;*/* } *因數*  
  
 不*帶正負號的整數*：： = {*數位*}  
  
 *大寫字母：：* = *A &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H &#124; I &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; P &#124; Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *使用者定義名稱* ：： = *字母*[*數位* &#124; *字母* &#124; *_*] .。。
