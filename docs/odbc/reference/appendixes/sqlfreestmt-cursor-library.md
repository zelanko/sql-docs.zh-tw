---
title: SQLFreeStmt （資料指標程式庫） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 07d56e9b77c7e7e34b0de98ef5704b26aa2b86dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199469"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (資料指標程式庫)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 本主題討論使用**SQLFreeStmt**資料指標程式庫中的函式。 如需一般資訊**SQLFreeStmt**，請參閱[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
 如果應用程式呼叫**SQLFreeStmt** SQL_UNBIND 選項之後，它會呼叫**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**，資料指標程式庫會傳回錯誤。 應用程式就可以解除繫結結果集資料行之前，必須呼叫**SQLCloseCursor**或是**SQLFreeStmt** SQL_CLOSE 選項。
