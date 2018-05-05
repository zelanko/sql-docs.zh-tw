---
title: SQLExtendedFetch （資料指標程式庫） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7b84c5dd3c39d31b94cfb12e6b116dd44963a0e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch （資料指標程式庫）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLExtendedFetch**資料指標程式庫中的函式。 如需一般資訊**SQLExtendedFetch**，請參閱[SQLExtendedFetch 函式](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 資料指標程式庫實作**SQLExtendedFetch**重複呼叫**SQLFetch**驅動程式中。  
  
 資料指標程式庫支援呼叫**SQLExtendedFetch**與*Sqlfetchscroll*要使用 sql_fetch_bookmark。  
  
 使用資料指標程式庫時，呼叫**SQLExtendedFetch**不得與呼叫**SQLFetchScroll**或**SQLFetch**。
