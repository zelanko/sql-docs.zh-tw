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
ms.openlocfilehash: 2cb829f065421a13d3c7df06c670808bc3d9d77c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064427"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLFetch**函數。 如需有關**SQLFetch**的一般資訊，請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 使用資料指標程式庫時， **SQLFetch**的呼叫不能與**SQLFetchScroll**或**SQLExtendedFetch**的呼叫混合使用。  
  
 如果呼叫**SQLFetch**時，SQL_ATTR_ROW_ARRAY_SIZE 設定為大於1的值，則資料指標程式庫會將呼叫傳遞給驅動程式。 如果驅動程式是 ODBC 2。*x*驅動程式，將會忽略資料列集大小，而**SQLFetch**的呼叫將會傳回單一資料列。  
  
 如果資料指標程式庫與 ODBC 2 搭配使用。*x*驅動程式：呼叫**SQLFetch**時，不會使用系結位移（如 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性所定義）。  
  
 載入資料指標程式庫時，應用程式無法呼叫**SQLFetch**來提取書簽資料行。 資料指標程式庫會將**SQLFetch**的呼叫傳遞至驅動程式，但資料指標程式庫會攔截呼叫以啟用書簽和系結書簽資料行的函數。
