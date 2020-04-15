---
title: 多個活動語句與連線 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8259967942f47b06c50a9043158f8b3b45c58d7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302427"
---
# <a name="multiple-active-statements-and-connections"></a>多個作用中陳述式和連線
某些驅動程式和 DBMS 限制一次處於活動狀態的語句和連接數。 這些數位可以小到一個。 有關詳細資訊,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式說明中的SQL_MAX_CONCURRENT_ACTIVITIES和SQL_MAX_DRIVER_CONNECTIONS選項,以及[敘述的句柄](../../../odbc/reference/develop-app/statement-handles.md)和[連接句柄](../../../odbc/reference/develop-app/connection-handles.md)。
