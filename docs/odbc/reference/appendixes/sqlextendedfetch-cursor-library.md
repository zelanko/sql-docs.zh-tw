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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3fd7d02d74b0e19d91871c5df7c9c5915d028f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064456"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLExtendedFetch**資料指標程式庫中的函式。 如需一般資訊**SQLExtendedFetch**，請參閱[SQLExtendedFetch 函式](../../../odbc/reference/syntax/sqlextendedfetch-function.md)。  
  
 資料指標程式庫會實作**SQLExtendedFetch**藉由重複呼叫**SQLFetch**驅動程式中。  
  
 資料指標程式庫支援呼叫**SQLExtendedFetch**具有*Sqlfetchscroll*要使用 sql_fetch_bookmark。  
  
 使用資料指標程式庫時，呼叫**SQLExtendedFetch**不得與呼叫**SQLFetchScroll**或是**SQLFetch**。
