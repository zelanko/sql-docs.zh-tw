---
title: 擷取的資料類型資訊與 SQLGetTypeInfo |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0a5377934d3487fcfdc58459e8d08e01c8bd21b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>SQLGetTypeInfo 與擷取的資料類型資訊
ODBC 從基礎 SQL 資料類型對應，以 ODBC 類型識別項是近似值，因為提供的函式 (**SQLGetTypeInfo**) 透過其驅動程式可以完整地描述每個資料來源中的 SQL 資料類型。 此函數會傳回結果集，其中每個資料列描述單一資料類型，例如名稱、 型別識別項、 有效位數、 小數位數和 null 屬性的特性。  
  
 這項資訊通常是由允許使用者建立及變更資料表的泛型應用程式所使用。 這類應用程式呼叫**SQLGetTypeInfo**擷取的資料類型資訊，並向使用者呈現部分或所有內容。 這類應用程式必須注意兩件事：  
  
-   一個以上的 SQL 資料型別可以對應至單一類型識別碼，這可以讓難以判斷要使用哪一個資料類型。 若要解決這個問題，，由類型識別項和第二個類型識別項的定義相似程度，會先排序結果集。 此外，資料來源定義資料類型的優先順序高於使用者定義資料類型。 例如，假設資料來源定義的整數和計數器的資料類型必須相同，不同之處在於計數器會自動遞增。 另外，假設使用者定義型別 WHOLENUM 是同義字的整數。 這兩種類型會對應至 SQL_INTEGER。 在**SQLGetTypeInfo**結果集，整數會出現在第一次，其後跟著 WHOLENUM，然後計數器。 WHOLENUM 出現之後的整數，因為它是使用者定義，但之前計數器因為多個緊密符合 SQL_INTEGER 定義輸入識別項。  
  
-   ODBC 不會定義資料型別名稱，以用於**CREATE TABLE**和**ALTER TABLE**陳述式。 應用程式應該改用所傳回的結果集之 TYPE_NAME 資料行中傳回的名稱**SQLGetTypeInfo**。 這麼做的原因是，雖然大部分的 SQL 不不同大部分 Dbms 之間，資料型別名稱不同極大的差異。 而不是強迫驅動程式來剖析 SQL 陳述式和標準的資料型別名稱取代 DBMS 專屬資料型別名稱，ODBC 會需要應用程式在第一次使用特定 DBMS 的名稱。  
  
 請注意， **SQLGetTypeInfo**不一定會描述所有的應用程式可能會遇到的資料類型。 特別是，結果集可能包含不直接支援的資料來源的資料類型。 比方說，目錄函數所傳回的結果集裡的資料行的資料類型會由 ODBC，這些資料類型可能不支援資料來源。 若要判斷結果集中的資料類型的特性，應用程式呼叫**SQLColAttribute**。
