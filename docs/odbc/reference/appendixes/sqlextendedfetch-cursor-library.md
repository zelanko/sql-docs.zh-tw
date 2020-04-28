---
title: SQLExtendedFetch （資料指標程式庫） |Microsoft Docs
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
ms.openlocfilehash: fe39b2d2cbbaf72ce3844c35187040589d1dac58
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302059"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (資料指標程式庫)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用**SQLExtendedFetch**函數。 如需有關**SQLExtendedFetch**的一般資訊，請參閱[SQLExtendedFetch 函數](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 資料指標程式庫會藉由重複呼叫驅動程式中的**SQLFetch**來執行**SQLExtendedFetch** 。  
  
 資料指標程式庫支援以 SQL_FETCH_BOOKMARK 的*FetchOrientation*呼叫**SQLExtendedFetch** 。  
  
 使用資料指標程式庫時， **SQLExtendedFetch**的呼叫不能與**SQLFetchScroll**或**SQLFetch**的呼叫混合使用。
