---
description: SQLNativeSql (資料指標程式庫)
title: SQLNativeSql (資料指標程式庫) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6046c8dabbc128a3afae772730cbad9eacc4b61c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424902"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (資料指標程式庫)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論如何在資料指標程式庫中使用 **SQLNativeSql** 函數。 如需 **SQLNativeSql**的一般資訊，請參閱 [SQLNativeSql 函數](../../../odbc/reference/syntax/sqlnativesql-function.md)。  
  
 如果驅動程式支援此函式，則資料指標程式庫會在驅動程式中呼叫 **SQLNativeSql** ，並將 SQL 語句傳遞給它。 若為定點更新、定位 delete 和 **SELECT FOR update** 語句，資料指標程式庫會先修改語句，然後再將它傳遞至驅動程式。  
  
> [!NOTE]  
>  資料指標程式庫不正確地傳回 SQLSTATE 34000 (不正確資料指標名稱) 如果資料指標名稱在**SQLNativeSql**的*InStatementText*引數中傳遞的定點更新或刪除語句中無效。 **SQLNativeSql** 不會傳回語法錯誤，這些錯誤只會在語句準備或執行時傳回。
