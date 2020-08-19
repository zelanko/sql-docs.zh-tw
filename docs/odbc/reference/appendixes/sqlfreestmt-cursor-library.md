---
description: SQLFreeStmt (資料指標程式庫)
title: SQLFreeStmt (資料指標程式庫) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9bc9ba1bc747f2c4408c308b13924afc8b3ba875
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448988"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLFreeStmt** 函數。 如需 **SQLFreeStmt**的一般資訊，請參閱 [SQLFreeStmt 函數](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
 如果應用程式在呼叫**SQLExtendedFetch**、 **SQLFetch**或**SQLFetchScroll**之後使用 SQL_UNBIND 選項呼叫**SQLFreeStmt** ，資料指標程式庫會傳回錯誤。 應用程式必須使用 SQL_CLOSE 選項來呼叫 **SQLCloseCursor** 或 **SQLFreeStmt** ，才能解除系結結果集資料行。
