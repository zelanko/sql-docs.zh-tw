---
description: 依書籤更新、刪除或擷取
title: 依書簽更新、刪除或提取 |Microsoft Docs
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
ms.openlocfilehash: 2202e3483e13848ccac7f7e6f21145ba9704a8b7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448945"
---
# <a name="updating-deleting-or-fetching-by-bookmark"></a>依書籤更新、刪除或擷取
書簽可以用來識別要在結果集中更新的資料、從結果集刪除的資料，或從結果集提取資料列集緩衝區的資料。 這些作業是藉由 SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK 的*選項*引數來呼叫**SQLBulkOperations**所執行。 這些作業中使用的書簽會儲存在資料列集緩衝區的資料行0中。 依書簽進行更新時，會將結果集資料行的資料更新為從資料列集緩衝區取出。 如需詳細資訊，請參閱 [使用 SQLBulkOperations 來更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。
