---
title: 中繼資料的使用方式為何？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3604e9f3bd47a10ae1a6e5ec401b198675c2d3e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149292"
---
# <a name="how-is-metadata-used"></a>中繼資料的使用方式為何？
應用程式需要大部分結果集作業的中繼資料。 例如，應用程式會使用資料行的資料類型來決定要繫結到該資料行的變數種類。 它會使用字元資料行的位元組長度來決定它必須顯示該資料行中的多少空間。 應用程式決定資料行之中繼資料的方式取決於應用程式的類型。  
  
 垂直應用程式使用的預先定義的資料表，並執行預先定義的作業，在這些資料表上。 因為這類應用程式的結果集中繼資料甚至會在撰寫應用程式，並受到應用程式開發人員之前定義，它可以是硬式編碼到應用程式。 例如，如果次序識別碼資料行在資料來源中定義為 4 位元組整數，應用程式永遠可以將 4 位元組整數繫結至該資料行。 當中繼資料在應用程式中寫入程式碼時，應用程式所使用的資料表變更通常意味著應用程式的程式碼變更。 這是很少發生問題，因為這類變更通常都會在應用程式的新版本的一部分。  
  
 如同垂直應用程式，自訂應用程式，通常使用預先定義的資料表，執行預先定義的作業，在這些資料表上進行相關的設定。 例如，應用程式可能會寫入在三個不同的資料來源; 之間傳送資料要傳送的資料通常稱為時撰寫應用程式。 因此，自訂應用程式也傾向具有硬式編碼的中繼資料。  
  
 泛型應用程式，尤其是那些支援臨機操作查詢，幾乎不會知道他們所建立的結果集的中繼資料。 因此，它們必須探索中繼資料，在執行階段使用的函式**SQLNumResultCols**， **SQLDescribeCol**，並**SQLColAttribute**，其中所述下一節[SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)。  
  
 所有的應用程式，不論其類型可以目錄函式所傳回的結果集的硬式編碼中繼資料。 本手冊的 [參考] 區段中定義這些結果集。
