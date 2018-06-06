---
title: Dbms 中的交易支援 |Microsoft 文件
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
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7095120f0a41bb4df5a3607c55abeb3a9da194f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="transaction-support-in-dbmss"></a>Dbms 中的交易支援
某些資料庫中，例如 dBASE、 Paradox 和 Btrieve，特別是桌面資料庫不支援交易。 支援交易的資料庫，之間，甚至沒有在不同的 SQL 陳述式可以是在交易中的變化。 如需詳細資訊，請參閱中的 SQL_TXN_CAPABLE 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。
