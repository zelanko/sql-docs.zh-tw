---
title: SQLFetch(游標庫) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bee83ccb5497888b57a45673599af6b92931a704
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298718"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在遊標庫中使用**SQLFetch**函數。 有關**SQLFetch 的**一般資訊,請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 使用游標庫時,對**SQLFetch 的**調用不能與**SQLFetchScroll 或** **SQL 擴展獲取的**調用混合。  
  
 如果將**SQLFetch**調用SQL_ATTR_ROW_ARRAY_SIZE設置為大於 1 的值,則游標庫將調用傳遞給驅動程式。 如果驅動程式是 ODBC 2。*x*驅動程式,將忽略行集大小,對**SQLFetch**的調用將返回一行數據。  
  
 如果游標庫與 ODBC 2 一起使用。*x*驅動程式,在調用**SQLFetch**時不使用綁定偏移量(由SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性定義)。  
  
 載入游標庫時,應用程式無法調用**SQLFetch**來獲取書籤列。 游標庫將**SQLFetch**的調用傳遞給驅動程式,但啟用書籤和綁定書籤列的函數調用被游標庫截獲。
