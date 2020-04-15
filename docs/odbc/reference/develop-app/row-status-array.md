---
title: 行狀態陣列 |微軟文件
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
ms.openlocfilehash: 60dead23fe0051c05698e094f37ddad96b2b337d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304288"
---
# <a name="row-status-array"></a>資料列狀態陣列
除了數據之外 **,SQLFetch**和**SQLFetchScroll**可以返回一個陣列,該陣列提供行集中每行的狀態。 此陣列透過SQL_ATTR_ROW_STATUS_PTR語句屬性指定。 此陣列由應用程式分配,並且必須具有SQL_ATTR_ROW_ARRAY_SIZE語句屬性指定的盡可能多的元素。 陣列中的值由**SQLBulk 操作****、SQLFetch、SQLFetchScroll**和**SQLSetPos**設定。 **SQLFetchScroll** 這些值描述行的狀態以及自上次提取行以來該狀態是否已更改。  
  
|行狀態陣列值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|該行已成功提取,自上次提取以來未更改。|  
|SQL_ROW_SUCCESS_WITH_INFO|該行已成功提取,自上次提取以來未更改。 但是,返回了有關該行的警告。|  
|SQL_ROW_ERROR|提取行時出錯。|  
|SQL_ROW_UPDATED|該行已成功提取,自上次提取以來已更新。 如果**SQLSetPos**再次提取或刷新該行,則其狀態將更改為新狀態。<br /><br /> 某些驅動程式無法檢測對數據的更改,因此無法返回此值。 要確定驅動程式是否可以檢測更新以重新提取行,應用程式使用SQL_ROW_UPDATES選項調用**SQLGetInfo。**|  
|SQL_ROW_DELETED|自上次提取行以來,該行已被刪除。|  
|SQL_ROW_ADDED|該行由**SQLBulk 操作**插入。 如果再次提取該行或由**SQLSetPos**刷新,則其狀態為SQL_ROW_SUCCESS。<br /><br /> 此值不是由**SQLFetch**或**SQLFetchScroll**設置的。|  
|SQL_ROW_NOROW|行集與結果集的末尾重疊,並且不會返回對應於行狀態陣列的此元素的行。|
