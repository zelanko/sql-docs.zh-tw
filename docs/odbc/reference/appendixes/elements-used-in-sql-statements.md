---
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
ms.openlocfilehash: 49a1cd54957426d4d14d84d43df670c8c3d96189
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307019"
---
# <a name="elements-used-in-sql-statements"></a>SQL 陳述式中使用的項目
下列元素會在先前所列的 SQL 語句中使用。  
  
## <a name="element"></a>元素  
 *基表-identifier* ：： =*使用者定義名稱*  
  
 *基表-名稱*：： =*基底-資料表識別碼*  
  
 *布林值-因素*：： = [NOT]*布林值-主要*  
  
 *布林值-primary* ：： = 比較 *-* 述詞 &#124; （*搜尋條件*）  
  
 *布林值*：： =*布林值因數*[和*布林值*]  
  
 *字元字串-常*值：： = ' ' {*character*} ... ' ' （*字元*是驅動程式/資料來源字元集中的任何字元。 若要在字元字串常值中包含單一常值（' '），請使用兩個常值引號字元 [' ' ']。）  
  
 資料*行識別碼*：： =*使用者定義名稱*  
  
 資料*行名稱*：： = [*資料表名稱*。]資料*行識別碼*  
  
 *比較-operator* ：： = < &#124; > &#124; \<= &#124; >= &#124; = &#124; <>  
  
 *比較-* 述詞：： =*運算式*比較-運算子運算式  
  
 *資料類型*：： =*字元字串類型*（*字元-字串類型*是 SQLGetTypeInfo 所傳回之結果集中 "" DATA_TYPE "" 資料行 SQL_CHAR 或 SQL_VARCHAR）的任何資料類型。  
  
 *數位*：： = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *動態參數*：： =？  
  
 *expression* ：： = term &#124; 運算式 {+&#124;-} 詞彙  
  
 *因素*：： = [*+*&#124;*-*]*主要*  
  
 *插入-值*：： =  
  
 *動態參數*  
  
 &#124;*常*值  
  
 &#124; Null  
  
 &#124; 使用者  
  
 *字母*：： =*小寫字母 &#124; 大寫*字母  
  
 *常*值：： =*字元字串常*值  
  
 *小寫字母*：： = a &#124; b &#124; c &#124; d &#124; e &#124; f &#124; g &#124; h &#124; &#124; j &#124; &#124; &#124; l &#124; m &#124; n &#124; o &#124; p &#124; q &#124; r &#124; &#124; &#124; x &#124; y &#124; z  
  
 *order by 子句*：： = order by*排序規格*[，*排序規格*] .。。  
  
 *primary* ：： = 資料*行名稱*  
  
 &#124;*動態參數*  
  
 &#124;*常*值  
  
 &#124; （*運算式*）  
  
 *搜尋-條件*：： =*布林值*[或*搜尋條件*]  
  
 *select-list* ：： = \* &#124;*選取-* 子清單 [，*選取-子清單*] .。。 （*select-list*不能包含參數）。  
  
 *select-子清單*：： = *expression*  
  
 *sort-規格*：： = {不*帶正負號的整數 &#124; 資料行名稱*} [*ASC &#124; DESC*]  
  
 *資料表識別碼*：： =*使用者定義名稱*  
  
 *資料表名稱*：： =*資料表識別碼*  
  
 *資料表參考*：： =*資料表名稱*  
  
 *資料表參考-list* ：： =*資料表*參考 [，*資料表參考*] .。。  
  
 *term* ：： =*因素*&#124;*詞彙*{\*&#124;*/*}*因素*  
  
 不*帶正負號-整數*：： = {*數位*}  
  
 *大寫的字母*：： = *A &#124; B &#124; C &#124; D &#124; E &#124; F &#124; G &#124; H &#124; I &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; P &#124; Q &#124; R &#124; &#124; &#124; X &#124; Y &#124; Z*  
  
 *使用者定義名稱*：： =*字母*[*數位*&#124;*字母*&#124; *_*] .。。
