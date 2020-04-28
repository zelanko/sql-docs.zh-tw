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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf536e06556e6b2e7b27f220d09a51f91b44d23c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304006"
---
# <a name="reserved-keyword-limitations"></a>保留關鍵字限制

請避免在您的 SQL 資料表或相關物件中使用任何 ODBC 保留關鍵字做為識別碼。 如果您必須使用保留關鍵字做為識別碼的情況，則必須以一對*倒引號*（'）括住識別碼。 *倒引號*的另一個名稱是「*後引號*」。

保留關鍵字限制也適用于任何簡短形式的保留關鍵字。

ODBC 保留關鍵字的清單可在下列位置取得：

- [ODBC 保留關鍵字](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)。

- 在 ODBC 程式設計*人員參考指南*中，請參閱[附錄 C： SQL 文法](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)。

