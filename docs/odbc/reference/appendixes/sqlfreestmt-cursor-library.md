---
title: SQLFreeStmt(游標庫) |微軟文件
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
ms.openlocfilehash: d78075593926c15dbaeb1904603b08e990f64983
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302019"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (資料指標程式庫)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。  
  
 本主題討論在游標庫中使用**SQLFreeStmt**函數。 有關**SQLFreeStmt 的**一般資訊,請參閱[SQLFreeStmt 函數](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
 如果應用程式在調用**SQLAtFetch、SQLFetch**或**SQLFetchScroll****SQLFetch**後使用SQL_UNBIND選項調用**SQLFreeStmt,** 則游標庫將傳回錯誤。 在取消綁定結果集列之前,應用程式必須使用SQL_CLOSE選項調用**SQLCloseCursor**或**SQLFreeStmt。**
