---
title: SQLSetScroll選項(可視化狐狸專業 ODBC 驅動程式) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19051fc83466bc40d72c029089cfe6ec45c20a08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299418"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援:部分  
  
 ODBC API 符合性:2 級  
  
 設置控制與語句句柄*hstmt*關聯的游標行為的選項。  
  
 可視化福克斯Pro ODBC驅動程式僅支援SQL_CONCUR_READ_ONLY;它不支援*fConcurrency*值SQL_CONCUR_ROWVER。 驅動程式將SQL_KEYSET_SIZE、SQL_CURSOR_DYNAMIC和SQL_CURSOR_KEYSET_DRIVEN轉換為具有警告ODBC_01S02SQL_SCROLL_STATIC。  
  
 關於詳細資訊,請參閱*ODBC 程式者參考*中的[SQLSetScroll 選項](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)。
