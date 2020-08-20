---
description: 中繼資料的使用方式為何？
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
ms.openlocfilehash: ca61677b0001ba4c39f81f80f6e3cbce26f27910
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476630"
---
# <a name="how-is-metadata-used"></a>中繼資料的使用方式為何？
應用程式需要大部分結果集作業的中繼資料。 例如，應用程式會使用資料行的資料類型來決定要繫結到該資料行的變數種類。 它會使用字元資料行的位元組長度，來決定從該資料行顯示資料需要多少空間。 應用程式決定資料行之中繼資料的方式取決於應用程式的類型。  
  
 垂直應用程式會使用預先定義的資料表，並在這些資料表上執行預先定義的作業。 由於這類應用程式的結果集中繼資料是在應用程式撰寫之前定義的，而且是由應用程式開發人員控制，因此可以硬式編碼到應用程式中。 例如，如果次序識別碼資料行在資料來源中定義為 4 位元組整數，應用程式永遠可以將 4 位元組整數繫結至該資料行。 當中繼資料在應用程式中寫入程式碼時，應用程式所使用的資料表變更通常意味著應用程式的程式碼變更。 這很少會造成問題，因為這類變更通常會做為應用程式新版本的一部分。  
  
 如同垂直應用程式，自訂應用程式通常會使用預先定義的資料表，並在這些資料表上執行預先定義的作業。 例如，應用程式可能會被撰寫成在三個不同的資料來源之間傳輸資料。寫入應用程式時，通常會知道要傳送的資料。 因此，自訂應用程式通常也會有硬式編碼的中繼資料。  
  
 泛型應用程式（特別是支援臨機操作查詢的應用程式）幾乎不知道其所建立之結果集的中繼資料。 因此，他們必須使用 **SQLNumResultCols**、 **SQLDescribeCol**和 **SQLColAttribute**等函式在執行時間探索中繼資料，如下一節所述： [SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)。  
  
 所有應用程式（不論其類型為何）都可以針對目錄函式所傳回的結果集，對中繼資料進行硬式編碼。 這些結果集會在此手冊的參考區段中定義。
