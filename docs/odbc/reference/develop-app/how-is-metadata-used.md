---
title: 方式是使用中繼資料？ | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c689b04d7772edbc25879f08a13d692a335f64c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="how-is-metadata-used"></a>方式是使用中繼資料？
應用程式需要大部分結果集作業的中繼資料。 例如，應用程式會使用資料行的資料類型來決定要繫結到該資料行的變數種類。 它會使用字元資料行的位元組長度來判斷多少空間，以便顯示該資料行的資料。 應用程式決定資料行之中繼資料的方式取決於應用程式的類型。  
  
 垂直應用程式，使用預先定義的資料表，並執行預先定義的作業，在這些資料表上。 應用程式甚至撰寫，並由應用程式開發人員控制之前，已經定義此類應用程式的結果集中繼資料，因為它可以是硬式編碼至應用程式。 例如，如果次序識別碼資料行在資料來源中定義為 4 位元組整數，應用程式永遠可以將 4 位元組整數繫結至該資料行。 當中繼資料在應用程式中寫入程式碼時，應用程式所使用的資料表變更通常意味著應用程式的程式碼變更。 這是很少會造成問題，因為這類變更通常都會是新發行的應用程式的一部分。  
  
 垂直應用程式，例如自訂應用程式，通常使用預先定義的資料表，並執行預先定義的作業，在這些資料表上。 例如，應用程式可能會寫入三個不同的資料來源; 之間傳送資料寫入應用程式時，通常已知要傳輸的資料。 因此，自訂的應用程式也會具有硬式編碼的中繼資料。  
  
 泛型應用程式，特別是那些支援臨機操作查詢，幾乎不會知道他們建立的結果集的中繼資料。 因此，它們必須探索中繼資料，在執行階段函式的使用**SQLNumResultCols**， **SQLDescribeCol**，和**SQLColAttribute**，即中描述下一節[SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)。  
  
 所有的應用程式，不論其類型可以目錄函數所傳回的結果集的硬式編碼中繼資料。 本手冊的參考章節中定義這些結果集。
