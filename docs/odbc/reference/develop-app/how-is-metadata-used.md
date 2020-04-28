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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbbba96fa2e99a2ccc0618f31e3b29e7d479f703
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300168"
---
# <a name="how-is-metadata-used"></a>中繼資料的使用方式為何？
應用程式需要大部分結果集作業的中繼資料。 例如，應用程式會使用資料行的資料類型來決定要繫結到該資料行的變數種類。 它會使用字元資料行的位元組長度來判斷要從該資料行顯示資料所需的空間量。 應用程式決定資料行之中繼資料的方式取決於應用程式的類型。  
  
 垂直應用程式會使用預先定義的資料表，並對這些資料表執行預先定義的作業。 因為這類應用程式的結果集中繼資料是在撰寫應用程式之前定義的，而且是由應用程式開發人員控制，所以它可以硬式編碼到應用程式中。 例如，如果次序識別碼資料行在資料來源中定義為 4 位元組整數，應用程式永遠可以將 4 位元組整數繫結至該資料行。 當中繼資料在應用程式中寫入程式碼時，應用程式所使用的資料表變更通常意味著應用程式的程式碼變更。 這很難解決，因為這類變更通常是應用程式新版本的一部分。  
  
 如同垂直應用程式，自訂應用程式通常會使用預先定義的資料表，並對這些資料表執行預先定義的作業。 例如，您可以撰寫應用程式，以在三個不同的資料來源之間傳輸資料;撰寫應用程式時，通常會知道要傳送的資料。 因此，自訂應用程式通常也會有硬式編碼的中繼資料。  
  
 一般應用程式（特別是支援特定查詢的應用程式）幾乎不知道它們所建立之結果集的中繼資料。 因此，他們必須在執行時間使用**SQLNumResultCols**、 **SQLDescribeCol**和**SQLColAttribute**函式來探索中繼資料，下一節[SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)將會說明這些功能。  
  
 所有應用程式（不論其類型為何）都可以硬式編碼目錄函數所傳回之結果集的中繼資料。 這些結果集會定義于此手冊的參考區段中。
