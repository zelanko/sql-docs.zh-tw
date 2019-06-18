---
title: 間隔資料類型長度 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16d0590d3297b52891bf399822ce984674022583
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188915"
---
# <a name="interval-data-type-length"></a>間隔資料類型長度
下列規則用來決定間隔資料類型以字元為單位的長度。 長度是以字元數表示。 位元組數目，取決於的字元集。 的長度會包含下列的值加在一起：  
  
-   每個欄位不是前置欄位的間隔中的兩個字元。  
  
-   前置的欄位中，或隱含的開頭有效位數的字元數。 如果未指定的前置字元的有效位數，預設值為 2。  
  
-   一個欄位之間的分隔符號字元。  
  
-   其中一個加上明示或默示的秒數有效位數。 如果未指定秒數有效位數，預設值為 6。  
  
 每個間隔資料類型的特定資料行長度值包含在[資料行大小](../../../odbc/reference/appendixes/column-size.md)。
