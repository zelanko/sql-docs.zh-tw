---
title: 資料列狀態陣列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d2a04f5052a0b686d3669c976ec7c4bee09e52b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706406"
---
# <a name="row-status-array"></a>資料列狀態陣列
除了資料之外， **SQLFetch**並**SQLFetchScroll**可以傳回陣列，提供資料列集中的每個資料列的狀態。 這個陣列會指定經由 sql_attr_row_status_ptr 設定陳述式屬性。 這個陣列由應用程式所配置，而且必須具有 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性所指定的項目數。 陣列中的值由設定**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，和**SQLSetPos。** 值會描述資料列和自上次擷取後，該狀態是否已變更的狀態。  
  
|資料列狀態陣列值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|資料列已成功擷取，而且尚未變更，因為它一次擷取。|  
|SQL_ROW_SUCCESS_WITH_INFO|資料列已成功擷取，而且尚未變更，因為它一次擷取。 不過，資料列相關的已傳回警告。|  
|SQL_ROW_ERROR|提取資料列時發生錯誤。|  
|SQL_ROW_UPDATED|已成功擷取的資料列，以及已經更新過一次擷取。 如果再次擷取或重新整理的資料列**SQLSetPos**，其狀態會變更為新的狀態。<br /><br /> 有些驅動程式無法偵測資料變更，且無法傳回此值。 若要判斷驅動程式是否可以偵測 refetched 的資料列更新，應用程式會呼叫**SQLGetInfo** SQL_ROW_UPDATES 選項。|  
|SQL_ROW_DELETED|因為一次擷取已刪除資料列。|  
|SQL_ROW_ADDED|已插入資料列**SQLBulkOperations**。 如果再次擷取或重新整理的資料列**SQLSetPos**，其狀態會是 SQL_ROW_SUCCESS。<br /><br /> 此值不由設定**SQLFetch**或是**SQLFetchScroll**。|  
|SQL_ROW_NOROW|重疊的資料列集結果集的結尾，並傳回任何資料列，對應至資料列狀態陣列的這個項目。|
