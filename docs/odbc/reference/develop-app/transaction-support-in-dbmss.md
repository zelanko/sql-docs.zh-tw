---
title: DBMS 中的事務支援 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6da6fdc819d8852aadcd7b672ef06e99d46c0ea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298003"
---
# <a name="transaction-support-in-dbmss"></a>DBMS 中的交易支援
某些資料庫,尤其是桌面資料庫(如 dBASE、Paradox 和 Btrieve)不支援事務。 即使在支援事務的資料庫中,事務中哪些類型的 SQL 語句也存在差異。 有關詳細資訊,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數說明中的SQL_TXN_CAPABLE選項。
