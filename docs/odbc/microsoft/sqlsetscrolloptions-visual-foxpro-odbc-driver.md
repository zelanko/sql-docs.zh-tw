---
title: SQLSetScrollOptions （Visual FoxPro ODBC 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 43f92a786bf2c4d77ad18c7ed6391abd4eff933d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions （Visual FoxPro ODBC 驅動程式）
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援： 部分  
  
 ODBC 應用程式開發介面相容性： 層級 2  
  
 設定選項來控制資料指標陳述式控制代碼相關聯的行為*hstmt*。  
  
 Visual FoxPro ODBC 驅動程式支援只 SQL_CONCUR_READ_ONLY;不支援*fConcurrency*值 SQL_CONCUR_ROWVER。 驅動程式將 SQL_KEYSET_SIZE、 SQL_CURSOR_DYNAMIC 和 SQL_CURSOR_KEYSET_DRIVEN SQL_SCROLL_STATIC 含有警告 ODBC_01S02。  
  
 如需詳細資訊，請參閱[SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)中*ODBC 程式設計人員參考*。
