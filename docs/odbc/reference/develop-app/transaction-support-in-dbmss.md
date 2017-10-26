---
title: "Dbms 中的交易支援 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 14c1519122484542b57e286c248c25c3fd6c0886
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="transaction-support-in-dbmss"></a>Dbms 中的交易支援
某些資料庫中，例如 dBASE、 Paradox 和 Btrieve，特別是桌面資料庫不支援交易。 支援交易的資料庫，之間，甚至沒有在不同的 SQL 陳述式可以是在交易中的變化。 如需詳細資訊，請參閱中的 SQL_TXN_CAPABLE 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。

