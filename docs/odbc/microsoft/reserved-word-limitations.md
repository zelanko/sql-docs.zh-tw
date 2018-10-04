---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 531a100fed389264d9af6a1733636792a3dc7920
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764486"
---
# <a name="reserved-keyword-limitations"></a>保留的關鍵字限制

請避免使用任何 ODBC 保留關鍵字當做識別項在您的 SQL 資料表或相關的物件。 時偶爾的情況下，您必須使用保留的關鍵字當做識別項，您就必須以一組住識別項*倒引號*（'）。 另一個名稱*倒*是*反引號*。

保留的關鍵字限制也適用於保留任何的關鍵字縮寫形式。

ODBC 保留關鍵字清單將會位於：

- [ODBC 保留關鍵字](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)。

- 在  *ODBC 程式設計人員參考指南*，請參閱[附錄 c: SQL 文法](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)。

