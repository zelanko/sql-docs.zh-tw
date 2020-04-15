---
title: 按書籤更新、刪除或提取 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e94a98bb577ef906afbb04539761fd07d15f772
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286148"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>依書籤更新、刪除或擷取
書籤可用於標識要在結果集中更新、從結果集中刪除或從結果集提取到行集緩衝區的數據。 這些操作透過呼叫**SQLBulk 操作**執行,*選項*參數為 SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK或SQL_FETCH_BY_BOOKMARK。 這些操作中使用的書籤存儲在行集緩衝區的第 0 列中。 按書籤更新時,將更新結果集列的數據從行集緩衝區檢索到。 有關詳細資訊,請參閱使用[SQLBulk 操作更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。
