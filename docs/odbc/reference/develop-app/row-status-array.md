---
title: "資料列狀態陣列 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 34fe599aee975dc0c01fc1fbc36f1bed6cab6b6b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="row-status-array"></a>資料列狀態陣列
除了資料之外， **SQLFetch**和**SQLFetchScroll**可以傳回資料列集中提供的每個資料列狀態的陣列。 此陣列是透過將 sql_attr_row_status_ptr 設定陳述式屬性指定。 此陣列由應用程式所配置，而且必須具有 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性所指定的元素。 陣列中的值由設定**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，和**SQLSetPos。** 這些值描述的資料列，以及上一次提取之後，該狀態是否已經變更的狀態。  
  
|資料列狀態陣列值|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|已成功擷取的資料列，以及自從上一次提取未變更。|  
|SQL_ROW_SUCCESS_WITH_INFO|已成功擷取的資料列，以及自從上一次提取未變更。 不過，資料列相關的傳回警告。|  
|SQL_ROW_ERROR|提取資料列時發生錯誤。|  
|SQL_ROW_UPDATED|已成功擷取的資料列，以及已經更新過一次提取。 如果再次擷取或重新整理的資料列**SQLSetPos**，其狀態變更為新的狀態。<br /><br /> 有些驅動程式無法偵測資料的變更，且無法傳回此值。 若要判斷驅動程式是否可以偵測 refetched 的資料列更新，應用程式呼叫**SQLGetInfo** SQL_ROW_UPDATES 選項。|  
|SQL_ROW_DELETED|資料列已經刪除，因為上一次提取。|  
|SQL_ROW_ADDED|資料列插入**SQLBulkOperations**。 如果再次擷取或重新整理的資料列**SQLSetPos**，其狀態是 SQL_ROW_SUCCESS。<br /><br /> 此值不由設定**SQLFetch**或**SQLFetchScroll**。|  
|SQL_ROW_NOROW|重疊的資料列集結果集的結尾，並傳回沒有資料列，對應到資料列狀態陣列的這個項目。|

