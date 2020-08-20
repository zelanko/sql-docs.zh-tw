---
description: DBMS 中的交易支援
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
ms.openlocfilehash: b8e0b3433e0f666af100cce5e72e36b685533b1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487451"
---
# <a name="transaction-support-in-dbmss"></a>DBMS 中的交易支援
某些資料庫（特別是 dBASE、Paradox 和 Btrieve 等桌面資料庫）不支援交易。 即使是支援交易的資料庫，在交易中有哪些類型的 SQL 語句可以有不同的變化。 如需詳細資訊，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函數描述中的 SQL_TXN_CAPABLE 選項。
