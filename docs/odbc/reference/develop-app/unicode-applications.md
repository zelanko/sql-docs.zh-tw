---
description: Unicode 應用程式
title: Unicode 應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee2db77c569876b008d21149c500aa0f1f009b7a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339154"
---
# <a name="unicode-applications"></a>Unicode 應用程式
您可以使用下列兩種方式之一，將應用程式重新編譯為 Unicode 應用程式：  
  
-   將 Unicode **#define** 包含在應用程式的 sqlucode.h .h 標頭檔中。  
  
-   使用編譯器的 Unicode 選項來編譯應用程式。  (針對不同的編譯器，此選項將會不同。 )   
  
 若要將 ANSI 應用程式轉換成 Unicode 應用程式，請撰寫應用程式來儲存和傳遞 Unicode 資料。 此外，呼叫支援 SQLPOINTER 引數的函式必須轉換成使用位元組計數。  
  
 將應用程式編譯為 Unicode 應用程式之後，如果應用程式呼叫 ODBC API 函式 (沒有尾碼) ，驅動程式管理員會將應用程式辨識為 Unicode 應用程式，並將函式呼叫轉換成 Unicode 函式，) 如果基礎驅動程式支援 Unicode *，則會* 將函式呼叫轉換為 unicode (函數。 當 ANSI 應用程式不使用尾碼進行函式呼叫時，如果基礎驅動程式支援 ANSI，驅動程式管理員就會將它轉換為 ANSI。 如果應用程式和驅動程式都支援相同的字元編碼，則驅動程式管理員會將呼叫傳遞至驅動程式 (並) ANSI 應用程式的特定例外狀況。  
  
 應用程式可以使用 *W* 尾碼) 和 ANSI 函式來呼叫這兩個 Unicode 函式 (，其 (不 *含尾碼) * 。 可以混合 Unicode 和 ANSI 函式呼叫。 但是，如果要使用資料指標程式庫，則無法混合 Unicode 和 ANSI 函式呼叫。 資料指標程式庫可以是 Unicode 或 ANSI，而不是混合。  
  
 您可以撰寫應用程式，讓它可以編譯為 Unicode 應用程式或 ANSI 應用程式。 在此情況下，字元資料類型可以宣告為 SQL_C_TCHAR。 如果應用程式編譯為 Unicode 應用程式，或是在編譯為 ANSI 應用程式的情況下插入 SQL_C_CHAR，則這是插入 SQL_C_WCHAR 的宏。 應用程式程式設計人員必須小心採用 SQLPOINTER 做為其引數的函式，因為長度引數的大小會隨著應用程式是 ANSI 或 Unicode 而變更)  (字串資料類型。  
  
 您可以使用下列三種方式之一來呼叫函式：做為僅限 Unicode 的函式呼叫，並以 *W* 尾碼)  (，做為僅限 *ANSI 的函數* 調用 (使用後置詞) ，或做為不含尾碼的 ODBC 函式呼叫。 函式的三種形式的引數相同。 只有具有 SQLCHAR \* 引數的函式或指向字串的 SQLPOINTER 引數才需要 Unicode 和 ANSI 格式。 如果函式具有可宣告為字元類型的引數（例如 **SQLBindCol** 或 **SQLGetData** (沒有 Unicode 和 ANSI) 格式），則引數可以宣告為 unicode 類型、ANSI 類型，或在 C 類型引數的情況下，SQL_C_TCHAR 宏。 如需詳細資訊，請參閱 [Unicode 資料](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 即使沒有 Unicode 驅動程式可供使用，應用程式也可以撰寫為 Unicode 應用程式。 驅動程式管理員會將 Unicode 函數和資料類型對應至 ANSI。 可以執行的 Unicode 與 ANSI 對應有一些限制。 Unicode 驅動程式使用 Unicode 驅動程式時，將會產生較佳的效能，而且會移除 Unicode 與 ANSI 對應的限制。
