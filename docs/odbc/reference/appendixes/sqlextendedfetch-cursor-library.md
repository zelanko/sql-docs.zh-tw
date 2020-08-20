---
description: SQLExtendedFetch (資料指標程式庫)
title: SQLExtendedFetch (資料指標程式庫) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab7d091dc6cee3630b5ed9b8bf3a3a479c0613e8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466010"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLExtendedFetch** 函數。 如需 **SQLExtendedFetch**的一般資訊，請參閱 [SQLExtendedFetch 函數](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 資料指標程式庫會在驅動程式中重複呼叫**SQLFetch** ，以執行**SQLExtendedFetch** 。  
  
 資料指標程式庫支援使用*FetchOrientation*的 SQL_FETCH_BOOKMARK 來呼叫**SQLExtendedFetch** 。  
  
 使用資料指標程式庫時，對 **SQLExtendedFetch** 的呼叫不能與 **SQLFetchScroll** 或 **SQLFetch**的呼叫混合。
