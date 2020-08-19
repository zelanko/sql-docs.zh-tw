---
description: 多個作用中陳述式和連線
title: 多個作用中語句和連接 |Microsoft Docs
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
ms.openlocfilehash: 56897dedbd1bf0d96dfa73f75a28db5f1ca46c43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429260"
---
# <a name="multiple-active-statements-and-connections"></a>多個作用中陳述式和連線
某些驅動程式和 Dbms 會限制可同時處於作用中狀態的語句和連接數目。 這些數位可以小到一。 如需詳細資訊，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函數描述中的 SQL_MAX_CONCURRENT_ACTIVITIES 和 SQL_MAX_DRIVER_CONNECTIONS 選項，以及 [語句控制碼](../../../odbc/reference/develop-app/statement-handles.md) 和 [連接控制碼](../../../odbc/reference/develop-app/connection-handles.md)。
