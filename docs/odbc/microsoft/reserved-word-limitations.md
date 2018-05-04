---
title: 保留字限制 |Microsoft 文件
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac61a7aa818ef3593fddc630d5027fbf7e4aa211
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="reserved-keyword-limitations"></a>限制保留的關鍵字

避免使用任何 ODBC 保留關鍵字做為您的 SQL 資料表或相關的物件中的識別項。 如果偶爾的情況下發生，您必須使用保留的關鍵字當做識別項，您必須具有一對括住識別碼*backticks* （'）。 另一個名稱*倒*是*反引號*。

保留的關鍵字限制也適用於保留任何的關鍵字縮寫形式。

ODBC 保留關鍵字清單將會位於：

- [ODBC 保留關鍵字](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)。

- 在*ODBC 程式設計人員參考指南*，請參閱[附錄 c: SQL 文法](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)。

