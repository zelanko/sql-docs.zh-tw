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
ms.openlocfilehash: 57b187bf4f14bd5c05f91a433fa331e954fa0fb9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020376"
---
# <a name="row-status-array"></a>資料列狀態陣列
除了資料以外， **SQLFetch**和**SQLFetchScroll**也可以傳回陣列，以提供資料列集中每個資料列的狀態。 這個陣列是透過 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指定。 這個陣列是由應用程式所配置，而且必須擁有與 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性所指定的數目一樣多的元素。 陣列中的值是由**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**和 SQLSetPos 所設定 **。** 這些值會描述資料列的狀態，以及該狀態自上次提取後是否已變更。  
  
|資料列狀態陣列值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|已成功提取資料列，而且自上次提取後尚未變更。|  
|SQL_ROW_SUCCESS_WITH_INFO|已成功提取資料列，而且自上次提取後尚未變更。 不過，傳回關於資料列的警告。|  
|SQL_ROW_ERROR|提取資料列時發生錯誤。|  
|SQL_ROW_UPDATED|已成功提取資料列，且自上次提取後已更新。 如果**SQLSetPos**再次提取或重新整理資料列，其狀態會變更為 [新狀態]。<br /><br /> 某些驅動程式無法偵測資料的變更，因此無法傳回此值。 若要判斷驅動程式是否可以偵測到根據資料列的更新，應用程式會使用 SQL_ROW_UPDATES 選項來呼叫**SQLGetInfo** 。|  
|SQL_ROW_DELETED|上次提取資料列之後，已將其刪除。|  
|SQL_ROW_ADDED|**SQLBulkOperations**插入資料列。 如果資料列再次提取或由**SQLSetPos**重新整理，其狀態會是 SQL_ROW_SUCCESS。<br /><br /> 這個值不是由**SQLFetch**或**SQLFetchScroll**所設定。|  
|SQL_ROW_NOROW|資料列集會重迭結果集的結尾，而且不會傳回雖然該值到資料列狀態陣列之這個元素的任何資料列。|
