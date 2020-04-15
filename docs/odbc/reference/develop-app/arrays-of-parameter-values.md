---
title: 參數值陣列 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298794"
---
# <a name="arrays-of-parameter-values"></a>參數值陣列
對於應用程序來說,傳遞參數陣列通常很有用。 例如,使用參數陣列和參數化**的INSERT**語句,應用程式可以同時插入多個行。 使用數組有幾個優點。 首先,網路流量減少,因為許多語句的數據在單個數據包中發送(如果數據源本機支援參數陣列)。 其次,某些數據源可以使用陣列執行 SQL 語句,比執行相同數量的單獨 SQL 語句更快。 最後,當數據存儲在陣列中時(就像螢幕數據通常的情況一樣),應用程式可以使用對**SQLBindparameter**的單一調用綁定特定列中的所有行,並通過執行單個語句來更新它們。  
  
 遺憾的是,支持參數陣列的數據源並不多。 但是,驅動程式可以通過為每個參數值集執行一次 SQL 語句來類比參數陣列。 這可能導致速度增加,因為驅動程式隨後可以準備計劃為每個參數集執行一次的語句。 它還可能導致更簡單的應用程式代碼。  
  
 此章節包含下列主題。  
  
-   [繫結參數陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
