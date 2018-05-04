---
title: 間隔資料類型長度 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
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
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34ad21f069bd88085b31bdb31850fc71ff57f87a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="interval-data-type-length"></a>間隔資料類型長度
下列規則可用來判斷是以字元為單位的間隔資料類型的長度。 長度是以字元數表示。 位元組數目，取決於的字元集。 該長度包含加在一起的下列值：  
  
-   不是 [前置] 欄位的間隔中每個欄位的兩個字元。  
  
-   將開頭的欄位，是明確或隱含的字元數開頭有效位數。 如果未指定的開頭有效位數，預設值為 2。  
  
-   一個欄位之間的分隔符號字元。  
  
-   其中一個加上明示或默示的秒數有效位數。 如果未指定秒數有效位數，預設值為 6。  
  
 中所包含的每個間隔資料類型的特定資料行長度值[資料行大小](../../../odbc/reference/appendixes/column-size.md)。
