---
description: 使用 SQLGetTypeInfo 擷取資料類型資訊
title: 使用 SQLGetTypeInfo 抓取資料類型資訊 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7135a6d149646c43eb93218d2ce8952930748c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476520"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>使用 SQLGetTypeInfo 擷取資料類型資訊
由於基礎 SQL 資料類型與 ODBC 類型識別碼之間的對應是近似的，因此 ODBC 會提供函數 (**SQLGetTypeInfo**) ，讓驅動程式可以完全描述資料來源中的每個 SQL 資料類型。 此函數會傳回結果集，每個資料列都會描述單一資料類型的特性，例如名稱、類型識別碼、有效位數、小數位數和 null 屬性。  
  
 這項資訊通常是由允許使用者建立和改變數據表的一般應用程式使用。 這類應用程式會呼叫 **SQLGetTypeInfo** 來取得資料類型資訊，然後將部分或全部呈現給使用者。 這類應用程式必須留意兩件事：  
  
-   有一個以上的 SQL 資料類型可以對應到單一類型識別碼，這可能會讓您難以判斷要使用哪種資料類型。 若要解決此問題，會先依類型識別碼排序結果集，然後接近程度至類型識別碼的定義。 此外，資料來源定義的資料類型優先于使用者定義的資料類型。 例如，假設資料來源將整數和計數器資料類型定義為相同，但該計數器是自動遞增的。 也假設使用者定義型別 WHOLENUM 是整數的同義字。 這兩種類型都會對應至 SQL_INTEGER。 在 **SQLGetTypeInfo** 結果集中，會先出現整數，後面接著 WHOLENUM 然後 COUNTER。 WHOLENUM 出現在整數之後，因為它是使用者定義的，但在計數器之前，因為它更接近 SQL_INTEGER 類型識別碼的定義。  
  
-   ODBC 不會定義要在 **CREATE TABLE** 和 **ALTER TABLE** 語句中使用的資料類型名稱。 相反地，應用程式應該使用 **SQLGetTypeInfo**所傳回之結果集的 TYPE_NAME 資料行中所傳回的名稱。 原因是，雖然大部分的 SQL 在 Dbms 之間都不會有太大的差異，但資料類型名稱的差異很大。 ODBC 會要求應用程式先使用 DBMS 特定的名稱，而不是強制驅動程式剖析 SQL 語句，並以 DBMS 特定的資料類型名稱取代標準資料類型名稱。  
  
 請注意， **SQLGetTypeInfo** 不一定會描述應用程式可能會遇到的所有資料類型。 尤其是，結果集可能包含資料來源不直接支援的資料類型。 例如，目錄函數所傳回之結果集中資料行的資料類型是由 ODBC 所定義，而且資料來源可能不支援這些資料類型。 若要判斷結果集中資料類型的特性，應用程式會呼叫 **SQLColAttribute**。
