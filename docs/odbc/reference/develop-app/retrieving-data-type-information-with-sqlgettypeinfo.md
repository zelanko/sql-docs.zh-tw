---
title: 使用 SQLGetTypeInfo 來抓取資料類型資訊 |Microsoft Docs
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
ms.openlocfilehash: c4f336a7ebfaf5e76ac464944900231c452809f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020554"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>使用 SQLGetTypeInfo 擷取資料類型資訊
因為從基礎 SQL 資料類型到 ODBC 類型識別碼的對應是近似值，所以 ODBC 會提供函式（**SQLGetTypeInfo**），而驅動程式可以透過這個函數來完整描述資料來源中的每個 SQL 資料類型。 此函式會傳回結果集，其中的每個資料列都會描述單一資料類型的特性，例如名稱、類型識別碼、有效位數、小數位數和 null 屬性。  
  
 一般應用程式會使用這項資訊，讓使用者能夠建立和改變數據表。 這類應用程式會呼叫**SQLGetTypeInfo**來抓取資料類型資訊，然後將其部分或全部呈現給使用者。 這類應用程式需要注意兩件事：  
  
-   一個以上的 SQL 資料類型可以對應到單一類型識別碼，這可能會讓您難以判斷要使用的資料類型。 若要解決這個問題，結果集會先依照類型識別碼和第二個排序，方法是接近程度至類型識別碼的定義。 此外，資料來源定義資料類型的優先順序高於使用者定義的資料類型。 例如，假設資料來源將整數和計數器資料類型定義為相同，不同之處在于計數器是自動遞增的。 另外，假設使用者定義型別 WHOLENUM 是整數的同義字。 這些類型都會對應到 SQL_INTEGER。 在**SQLGetTypeInfo**結果集中，會先出現 INTEGER，後面接著 WHOLENUM，然後是 COUNTER。 WHOLENUM 會出現在 INTEGER 之後，因為它是使用者定義的，但在 COUNTER 之前，因為它更符合 SQL_INTEGER 類型識別碼的定義。  
  
-   ODBC 不會定義要在**CREATE TABLE**和**ALTER TABLE**語句中使用的資料類型名稱。 相反地，應用程式應該使用**SQLGetTypeInfo**所傳回之結果集的 TYPE_NAME 資料行中所傳回的名稱。 這是因為雖然大部分的 SQL 在 Dbms 之間並不會有太大的差異，但資料類型名稱的差異也會有所不同。 ODBC 不會強制驅動程式剖析 SQL 語句，並將標準資料類型名稱取代為 DBMS 特定的資料類型名稱，因此，ODBC 要求應用程式在第一次使用 DBMS 特定的名稱。  
  
 請注意， **SQLGetTypeInfo**不一定會描述應用程式可能會遇到的所有資料類型。 特別是，結果集可能包含資料來源不直接支援的資料類型。 例如，目錄函數所傳回之結果集中資料行的資料類型是由 ODBC 所定義，而資料來源可能不支援這些資料類型。 若要判斷結果集中資料類型的特性，應用程式會呼叫**SQLColAttribute**。
