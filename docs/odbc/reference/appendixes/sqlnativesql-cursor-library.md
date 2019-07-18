---
title: SQLNativeSql （資料指標程式庫） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a8c42efbd87296cf7157d75d1848e4655247818
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125706"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLNativeSql**資料指標程式庫中的函式。 如需一般資訊**SQLNativeSql**，請參閱[SQLNativeSql 函數](../../../odbc/reference/syntax/sqlnativesql-function.md)。  
  
 如果驅動程式支援此函式，資料指標程式庫就會呼叫**SQLNativeSql**驅動程式中，並將它傳遞的 SQL 陳述式。 定位更新，位於 [刪除]，並**選取用於更新**陳述式中，資料指標程式庫修改陳述式，再將它傳遞至驅動程式。  
  
> [!NOTE]  
>  資料指標程式庫不正確地傳回 SQLSTATE 34000 （無效的資料指標名稱），如果資料指標名稱中無效的定位的 update 或 delete 陳述式中傳入*InStatementText*引數**SQLNativeSql**. **SQLNativeSql**不是要傳回語法錯誤，只有在陳述式準備或執行時才會傳回。
