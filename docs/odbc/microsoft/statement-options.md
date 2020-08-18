---
description: 陳述式選項
title: 語句選項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 024fc10441f3b24da33d5742fdd15454561187c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449140"
---
# <a name="statement-options"></a>陳述式選項
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 這些選項可讓您自訂應用程式內的特定執行語句。  
  
|語句選項|注意|  
|----------------------|-----------|  
|SQL_BIND_TYPE|不能超過2147483647個位元組或可用的記憶體。|  
|SQL_CONCURRENCY|如需允許的值，請參閱資料 [指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_CURSOR_TYPE|驅動程式不允許 SQL_CURSOR_DYNAMIC。 如需詳細資訊，請參閱 [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) 。 如需允許的值，請參閱資料 [指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_GET_BOOKMARK|傳回32位整數值，這是目前記錄號碼的書簽。 僅限 Get;無法設定。|  
|SQL_KEYSET_SIZE|只能設定為0。|  
|SQL_MAX_ROWS|從結果集傳回的最大資料列數。|  
|SQL_ROW_NUMBER|傳回32位整數，指定結果集內目前資料列的位置。 僅限 Get;無法設定。|  
|SQL_ROWSET_SIZE|不能超過4294967296個數據列;不過，您的電腦中必須有足夠的虛擬記憶體，才能處理您的要求。|  
|SQL_USE_BOOKMARKS|支援將 SQL_USE_BOOKMARKS 設定為 SQL_UB_ON 並公開固定長度的書簽。|
