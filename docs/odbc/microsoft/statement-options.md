---
title: 陳述式選項 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe57ffa0d7628601fcb6dd19218715b32a57322b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47829476"
---
# <a name="statement-options"></a>陳述式選項
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 這些選項可讓自訂應用程式內的特定執行陳述式。  
  
|陳述式選項|注意|  
|----------------------|-----------|  
|SQL_BIND_TYPE|不能超過 2,147,483,647 個位元組或可用的記憶體。|  
|SQL_CONCURRENCY|允許的值，請參閱[資料指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_CURSOR_TYPE|驅動程式不允許 SQL_CURSOR_DYNAMIC。 請參閱[SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md)如需詳細資訊。 允許的值，請參閱[資料指標類型和並行組合](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)。|  
|SQL_GET_BOOKMARK|傳回 32 位元整數值，是目前的記錄數目的書籤。 僅; get無法設定。|  
|SQL_KEYSET_SIZE|可以是只能設為 0。|  
|SQL_MAX_ROWS|若要從結果中傳回的資料列的數目上限設定。|  
|SQL_ROW_NUMBER|傳回 32 位元整數，指定目前的資料列結果集內的位置。 僅; get無法設定。|  
|SQL_ROWSET_SIZE|不能超過 4,294,967,296 的資料列;不過，您必須將虛擬記憶體不足，無法在您的電腦，以處理您的要求。|  
|SQL_USE_BOOKMARKS|支援 SQL_USE_BOOKMARKS 設 SQL_UB_ON，並公開固定長度書籤。|
