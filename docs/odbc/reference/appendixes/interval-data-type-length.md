---
description: 間隔資料類型長度
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 589a13e0f0b2c6e6e42ade0f0dc32415556a0efc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483277"
---
# <a name="interval-data-type-length"></a>間隔資料類型長度
下列規則是用來判斷間隔資料類型的長度（以字元為單位）。 長度以字元數表示。 以字元集為依據的位元組數目。 長度包含下列已新增的值：  
  
-   間隔中不是前置欄位的每個欄位都有兩個字元。  
  
-   若為前置欄位，即為快速或隱含前置精確度的字元數。 如果未指定前置精確度，則預設值為2。  
  
-   欄位之間的分隔符號會有一個字元。  
  
-   其中一個是快速或隱含的秒數有效位數。 如果未指定秒數有效位數，則預設值為6。  
  
 每個間隔資料類型的特定資料行長度值都包含在資料 [行大小](../../../odbc/reference/appendixes/column-size.md)中。
