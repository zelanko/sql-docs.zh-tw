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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300168"
---
# <a name="how-is-metadata-used"></a>中繼資料的使用方式為何？
應用程式需要大部分結果集作業的中繼資料。 例如，應用程式會使用資料行的資料類型來決定要繫結到該資料行的變數種類。 它使用字元列的位元組長度來確定顯示該列資料所需的空間。 應用程式決定資料行之中繼資料的方式取決於應用程式的類型。  
  
 垂直應用程式使用預定義的表,並對這些表執行預定義的操作。 由於此類應用程式的結果集元數據是在應用程式編寫之前定義的,並且由應用程式開發人員控制,因此可以硬編碼到應用程式中。 例如，如果次序識別碼資料行在資料來源中定義為 4 位元組整數，應用程式永遠可以將 4 位元組整數繫結至該資料行。 當中繼資料在應用程式中寫入程式碼時，應用程式所使用的資料表變更通常意味著應用程式的程式碼變更。 這很少是一個問題,因為此類更改通常是作為應用程式的新版本的一部分進行的。  
  
 與垂直應用程式一樣,自定義應用程式通常使用預定義的表,並在這些表上執行預定義的操作。 例如,可以編寫應用程式來在三個不同的數據源之間傳輸數據;寫入應用程式時,通常知道要傳輸的數據。 因此,自定義應用程式也往往具有硬編碼的元數據。  
  
 通用應用程式(尤其是支援臨時查詢的應用程式)幾乎永遠不會知道它們創建的結果集的元數據。 因此,他們必須使用**SQLNumResultCols、SQLDescribeCol**和**SQLColAttribute**等函數在執行時發現元數據,下一節將介紹[SQLDescribeCol 和 SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)。 **SQLDescribeCol**  
  
 所有應用程式(無論其類型如何)都可以對目錄函數返回的結果集的元數據進行硬編碼。 這些結果集在本手冊的參考部分中定義。
