---
title: 多個作用中陳述式和連線 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b548b6d1b1aa7e7b260abcc9f507e2dbd566e7c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912643"
---
# <a name="multiple-active-statements-and-connections"></a>多個作用中陳述式和連線
一些驅動程式和 Dbms 限制之陳述式和每次最多可處於作用中的連接數目。 這些數字可以很小，成為其中一員。 如需詳細資訊，請參閱 「 SQL_MAX_CONCURRENT_ACTIVITIES 和 SQL_MAX_DRIVER_CONNECTIONS 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述，和[陳述式會處理](../../../odbc/reference/develop-app/statement-handles.md)和[連接控制代碼](../../../odbc/reference/develop-app/connection-handles.md)。
