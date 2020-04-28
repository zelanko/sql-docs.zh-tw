---
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
ms.openlocfilehash: eb9389c769e3a7bb0c39959a559531e8051a7bec
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298794"
---
# <a name="arrays-of-parameter-values"></a>參數值陣列
應用程式傳遞參數陣列通常會很有用。 例如，使用參數陣列和參數化**INSERT**語句，應用程式可以一次插入多個資料列。 使用陣列有幾個優點。 首先，網路流量會降低，因為許多語句的資料會以單一封包傳送（如果資料來源是以原生方式支援參數陣列）。 第二，有些資料來源可以使用陣列執行 SQL 語句的速度，比執行相同數目的個別 SQL 語句更快。 最後，當資料儲存在陣列中（通常是螢幕資料的情況）時，應用程式可以系結特定資料行中的所有資料列與**SQLBindParameter**的單一呼叫，並藉由執行單一語句來加以更新。  
  
 可惜的是，不是有許多資料來源支援參數陣列。 不過，驅動程式可以針對每一組參數值執行一次 SQL 語句，以模擬參數陣列。 這可能會導致速度增加，因為驅動程式可以準備它打算針對每個參數集執行一次的語句。 它也可能會導致應用程式代碼更簡單。  
  
 此章節包含下列主題。  
  
-   [繫結參數陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
