---
title: 間隔資料類型長度 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68bb4daa47cb58d5a0ff7b680a2d2154fb14b345
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284317"
---
# <a name="interval-data-type-length"></a>間隔資料類型長度
以下規則用於確定以字元為單位的間隔數據類型的長度。 長度以字元數表示。 位元組數取決於字元集。 長度包括新增在一起的以下值:  
  
-   間隔中每個欄位的兩個字元,而不是前導欄位。  
  
-   對於前導欄位,表示表示或隱式前導精度的字元數。 如果未指定前導精度,則預設值為 2。  
  
-   欄位之間的分隔符的一個字元。  
  
-   一加上明示或隱含秒精度。 如果未指定秒精度,則預設值為 6。  
  
 每個間隔數據類型的特定列長度值包含在[列大小](../../../odbc/reference/appendixes/column-size.md)中。
