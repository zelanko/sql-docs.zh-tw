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
ms.openlocfilehash: a456db12ddb2594dc7b4c9e4f5c26e9cb4245621
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947583"
---
# <a name="interval-data-type-length"></a>間隔資料類型長度
下列規則是用來判斷 interval 資料類型的長度（以字元為單位）。 長度以字元數表示。 位元組數目取決於字元集。 長度包含下列新增的值：  
  
-   間隔中不是前置欄位的每個欄位都有兩個字元。  
  
-   對於前置欄位，這是快速或隱含前置精確度的字元數。 如果未指定前置精確度，預設值為2。  
  
-   欄位之間分隔符號的一個字元。  
  
-   一個加上快速或隱含的秒數有效位數。 如果未指定秒數有效位數，則預設值為6。  
  
 每個間隔資料類型的特定資料行長度值會包含在資料[行大小](../../../odbc/reference/appendixes/column-size.md)中。
