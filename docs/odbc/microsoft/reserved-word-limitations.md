---
description: 保留關鍵字限制
title: 保留字限制 |Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07917cbe056b38be42e4697fcef52935bae3efe3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449290"
---
# <a name="reserved-keyword-limitations"></a>保留關鍵字限制

避免使用任何 ODBC 保留關鍵字做為 SQL 資料表或相關物件中的識別碼。 如果在您必須使用保留關鍵字做為識別碼的情況下發生異常狀況，您必須使用一對 *倒引號* (') 來括住識別碼。 *倒引號*的另一個名稱為*後引號*。

保留關鍵字限制也適用于保留關鍵字的任何速記形式。

ODBC 保留關鍵字的清單可于下列位置取得：

- [ODBC 保留關鍵字](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)。

- 請參閱《 ODBC 程式設計 *人員參考指南》* 中的 [附錄 C： SQL 文法](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)。

