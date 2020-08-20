---
description: SQLFetch (資料指標程式庫)
title: SQLFetch (資料指標程式庫) |Microsoft Docs
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
ms.openlocfilehash: ce9da3c0c5b95be4336c58896b17b6ba5daf6443
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466000"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLFetch** 函數。 如需 **SQLFetch**的一般資訊，請參閱 [SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 使用資料指標程式庫時，對 **SQLFetch** 的呼叫不能與 **SQLFetchScroll** 或 **SQLExtendedFetch**的呼叫混合。  
  
 如果呼叫 **SQLFetch** 時，SQL_ATTR_ROW_ARRAY_SIZE 將設定為大於1的值，則資料指標程式庫會將呼叫傳遞給驅動程式。 如果驅動程式是 ODBC 2。*x* 驅動程式，資料列集大小將會被忽略，而且對 **SQLFetch** 的呼叫將會傳回單一資料列。  
  
 如果資料指標程式庫與 ODBC 2 搭配使用。*x* 驅動程式，呼叫 **SQLFetch** 時，不會使用 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句) 屬性所定義的系結位移 (。  
  
 載入資料指標程式庫時，應用程式無法呼叫 **SQLFetch** 來提取書簽資料行。 資料指標程式庫會將 **SQLFetch** 的呼叫傳遞至驅動程式，但函式呼叫以啟用書簽，而系結書簽資料行則是由資料指標程式庫所攔截。
