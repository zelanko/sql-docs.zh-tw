---
description: 參數值陣列
title: 參數值的陣列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 230f15f1c9cae0509ba7d616ab61ed5d8d7a370b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483111"
---
# <a name="arrays-of-parameter-values"></a>參數值陣列
這通常適用于應用程式傳遞參數陣列。 例如，使用參數陣列和參數化的 **INSERT** 語句，應用程式可以一次插入多個資料列。 使用陣列有幾個優點。 首先，會降低網路流量，因為許多語句的資料會在單一封包中傳送 (如果資料來源支援原生) 的參數陣列。 其次，有些資料來源可以使用陣列來執行 SQL 語句，其速度比執行相同數目的不同 SQL 語句更快。 最後，當資料儲存在陣列中，通常是螢幕資料的情況，應用程式可以使用 **SQLBindParameter** 的單一呼叫來系結特定資料行中的所有資料列，並藉由執行單一語句來更新它們。  
  
 可惜的是，不是許多資料來源都支援參數陣列。 不過，驅動程式可以針對每一組參數值執行一次 SQL 語句來模擬參數陣列。 這可能會加快速度的增加，因為驅動程式可以準備要針對每個參數集執行一次的語句。 它也可能會導致更簡單的應用程式程式碼。  
  
 此章節包含下列主題。  
  
-   [繫結參數陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
