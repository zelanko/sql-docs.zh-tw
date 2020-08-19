---
description: 傳回 SQL_NO_DATA
title: 傳回 SQL_NO_DATA |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24efdd88d16ba31a2b70dfb75ad21adee08c6f1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424970"
---
# <a name="returning-sql_no_data"></a>傳回 SQL_NO_DATA
當 ODBC 2.x*應用程式**使用 odbc 3.x*驅動程式呼叫**SQLExecDirect**、 **SQLExecute**或**SQLParamData**，且已執行搜尋的 update 或 delete 語句時，但不會影響資料來源中的任何資料列時 *，ODBC 3.x*驅動程式應該會傳回 SQL_SUCCESS。 使用*odbc 3.x 驅動程式*來呼叫**SQLExecDirect**、 **SQLExecute**或**SQLParamData**時，*如果 ODBC 3.x 應用程式*使用相同的結果 *，odbc 3.x 驅動程式應該*會傳回 SQL_NO_DATA。  
  
 如果在語句批次中搜尋的 update 或 delete 語句不會影響資料來源中的任何資料列， **SQLMoreResults** 就會傳回 SQL_SUCCESS。 它無法傳回 SQL_NO_DATA，因為這表示沒有其他結果，而是搜尋的 update/delete 結果不會影響任何資料列。
