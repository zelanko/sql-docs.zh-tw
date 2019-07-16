---
title: SQLSetScrollOptions (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3746d9cea2ce5ffb7d03424d7cda4fa1889aabc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905386"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：Partial  
  
 ODBC API 相容性：層級 2  
  
 設定選項來控制資料指標行為的陳述式控制代碼相關聯*hstmt*。  
  
 Visual FoxPro ODBC Driver 支援只 SQL_CONCUR_READ_ONLY;不支援*fConcurrency*值 SQL_CONCUR_ROWVER。 驅動程式會將 SQL_KEYSET_SIZE、 SQL_CURSOR_DYNAMIC 和 SQL_CURSOR_KEYSET_DRIVEN SQL_SCROLL_STATIC 警告 ODBC_01S02。  
  
 如需詳細資訊，請參閱 < [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)中*ODBC 程式設計人員參考*。
