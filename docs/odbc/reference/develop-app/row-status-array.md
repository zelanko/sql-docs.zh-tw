---
description: 資料列狀態陣列
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8067aaf8724a6634d165d53743cbd0ef2015f6bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465631"
---
# <a name="row-status-array"></a>資料列狀態陣列
除了資料外， **SQLFetch** 和 **SQLFetchScroll** 也可以傳回陣列，以提供資料列集中每個資料列的狀態。 這個陣列是透過 SQL_ATTR_ROW_STATUS_PTR 語句屬性來指定。 這個陣列是由應用程式所配置，而且必須擁有 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性所指定的多個元素。 陣列中的值是由 **SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**和 SQLSetPos 所設定 **。** 這些值會描述資料列的狀態，以及自從上次提取之後該狀態是否已變更。  
  
|資料列狀態陣列值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|資料列已成功提取，自上次提取之後尚未變更。|  
|SQL_ROW_SUCCESS_WITH_INFO|資料列已成功提取，自上次提取之後尚未變更。 但是，傳回有關資料列的警告。|  
|SQL_ROW_ERROR|提取資料列時發生錯誤。|  
|SQL_ROW_UPDATED|資料列已成功提取，且自上次提取之後已更新。 如果 **SQLSetPos**再次提取或重新整理資料列，它的狀態會變更為新的狀態。<br /><br /> 某些驅動程式無法偵測到對資料所做的變更，因此無法傳回此值。 為了判斷驅動程式是否可以偵測根據資料列的更新，應用程式會使用 SQL_ROW_UPDATES 選項來呼叫 **SQLGetInfo** 。|  
|SQL_ROW_DELETED|已刪除資料列，因為它是上次提取的資料列。|  
|SQL_ROW_ADDED|**SQLBulkOperations**插入資料列。 如果資料列再次提取或由 **SQLSetPos**重新整理，其狀態會是 SQL_ROW_SUCCESS。<br /><br /> **SQLFetch**或**SQLFetchScroll**不會設定這個值。|  
|SQL_ROW_NOROW|資料列集重迭了結果集的結尾，而且沒有傳回任何資料列來對應至資料列狀態陣列的這個元素。|
