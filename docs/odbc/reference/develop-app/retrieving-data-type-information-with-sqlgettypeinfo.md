---
title: 擷取的資料型別資訊使用 SQLGetTypeInfo |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c69113e4bb5457cb997f832179e5c1aab2841d82
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518872"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>使用 SQLGetTypeInfo 擷取資料類型資訊
ODBC 從基礎 SQL 資料類型對應，以 ODBC 類型識別碼為估計值，因為提供的函式 (**SQLGetTypeInfo**) 透過讓驅動程式可以完整地描述每個資料來源中的 SQL 資料類型。 此函式會傳回結果集，其中每個資料列描述單一資料類型，例如名稱、 型別識別項、 有效位數、 小數位數和 null 屬性的特性。  
  
 這項資訊通常會使用允許使用者建立及變更資料表的泛型應用程式。 這類應用程式會呼叫**SQLGetTypeInfo**擷取的資料型別資訊，並向使用者顯示的部分或所有。 這類應用程式必須要注意兩件事：  
  
-   一個以上的 SQL 資料型別可以對應為單一類型的識別項，可以使其難以決定要使用哪一個資料類型。 若要解決這個問題，，由型別識別項和第二個類型識別項的定義相似程度，會先排序結果集。 此外，資料來源定義資料類型的優先順序高於使用者定義資料類型。 例如，假設資料來源定義的整數和計數器的資料類型必須相同，不同之處在於計數器會遞增。 另外，假設使用者定義的型別 WHOLENUM 是整數的同義字。 每一種類型會對應至 SQL_INTEGER。 在  **SQLGetTypeInfo**結果集，整數會顯示第一，後面接著 WHOLENUM，然後計數器。 WHOLENUM 出現之後的整數，因為它是使用者定義，但計數器之前因為更密切符合的 SQL_INTEGER 定義類型的識別項。  
  
-   ODBC 不會定義資料型別名稱，以用於**CREATE TABLE**並**ALTER TABLE**陳述式。 相反地，應用程式應該使用所傳回的結果集之 TYPE_NAME 資料行中傳回的名稱**SQLGetTypeInfo**。 原因是，雖然大部分的 SQL 不不同 Dbms 跨許多，資料型別名稱不同極大的差異。 而不是強迫驅動程式，以剖析 SQL 陳述式，並以特定 DBMS 的資料型別名稱取代標準的資料型別名稱，ODBC 會需要應用程式一開始使用特定 DBMS 的名稱。  
  
 請注意， **SQLGetTypeInfo**不一定是描述的所有應用程式可能會遇到的資料類型。 特別是，結果集可能包含不直接支援的資料來源的資料類型。 比方說，目錄函數所傳回的結果集裡的資料行的資料類型由 ODBC 定義，這些資料類型可能不支援資料來源。 若要判斷結果集中的資料類型的特性，應用程式會呼叫**SQLColAttribute**。
