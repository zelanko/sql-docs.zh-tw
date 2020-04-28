---
title: Dbms 中的交易支援 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298003"
---
# <a name="transaction-support-in-dbmss"></a>DBMS 中的交易支援
某些資料庫（尤其是 dBASE、Paradox 和 Btrieve 等桌面資料庫）不支援交易。 即使是支援交易的資料庫，在交易中可以有何種 SQL 語句的變化。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述中的 SQL_TXN_CAPABLE 選項。
