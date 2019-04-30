---
title: SQLFetch （資料指標程式庫） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 487a6b357d21ee675fa9594d32c7a2bb7c66e400
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199480"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLFetch**資料指標程式庫中的函式。 如需一般資訊**SQLFetch**，請參閱[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 使用資料指標程式庫時，呼叫**SQLFetch**不得與呼叫**SQLFetchScroll**或是**SQLExtendedFetch**。  
  
 如果**SQLFetch**稱為使用 SQL_ATTR_ROW_ARRAY_SIZE 設定為值大於 1，資料指標程式庫會將傳遞至驅動程式呼叫。 如果驅動程式的 ODBC 2。*x*驅動程式，將略過資料列集大小和呼叫**SQLFetch**會傳回單一資料列。  
  
 如果資料指標程式庫會使用 ODBC 2。*x*驅動程式，位移 （如 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性所定義） 的繫結不是使用的時機**SQLFetch**呼叫。  
  
 應用程式載入資料指標程式庫時，無法呼叫**SQLFetch**擷取書籤資料行。 資料指標程式庫會傳遞至呼叫**SQLFetch**透過驅動程式，但函式呼叫啟用書籤和書籤資料行繫結會攔截資料指標程式庫。
