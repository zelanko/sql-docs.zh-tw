---
description: SQLSetScrollOptions (Visual FoxPro ODBC Driver)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0e7cecfb0ce7640575cb69f1e84e805a884b57b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421632"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援：部分  
  
 ODBC API 一致性：層級2  
  
 設定選項，這些選項會控制與語句控制碼 *hstmt*相關聯之資料指標的行為。  
  
 Visual FoxPro ODBC 驅動程式僅支援 SQL_CONCUR_READ_ONLY;它不支援 SQL_CONCUR_ROWVER 的 *fConcurrency* 值。 驅動程式會將 SQL_KEYSET_SIZE、SQL_CURSOR_DYNAMIC 和 SQL_CURSOR_KEYSET_DRIVEN 轉換成 SQL_SCROLL_STATIC，並出現警告 ODBC_01S02。  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) 。
