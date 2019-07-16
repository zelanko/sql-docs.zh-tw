---
title: 更新、 刪除或擷取依書籤 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating by bookmarks [ODBC]
- result sets [ODBC], bookmarks
- fetches [ODBC], by bookmarks [ODBC]
- deleting by bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: e2ee58d7-c28f-435f-b537-06207215dd2f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce43cb1d5563128e840aa3c0df26190524774a38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091628"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>依書籤更新、刪除或擷取
書籤可用來識別要更新在結果集中，從結果集，或從結果集資料列集的緩衝區中提取已刪除的資料。 這些作業都由呼叫**SQLBulkOperations**具有*選項*SQL_UPDATE_BY_BOOKMARK、 SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK 的引數。 這些作業中使用書籤會儲存在資料行 0 的資料列集的緩衝區。 在更新依書籤時，結果集資料行的資料會更新為會從資料列集的緩衝區。 如需詳細資訊，請參閱 <<c0> [ 更新資料的資料使用 SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。
