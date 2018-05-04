---
title: 參數值的陣列 |Microsoft 文件
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
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38dc5fb0ed2286b3077e6198bc978808063b5d2f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="arrays-of-parameter-values"></a>參數值的陣列
通常會很有用的應用程式，以傳遞的參數陣列。 例如，使用參數和參數化的陣列**插入**陳述式中，應用程式可以一次插入的資料列數目。 有數個優點，以使用陣列。 首先，因為在單一封包中傳送多個陳述式的資料 （如果資料來源原生支援的參數陣列） 可以降低網路流量。 第二，某些資料來源可執行速度比執行相同數目的不同的 SQL 陳述式使用陣列的 SQL 陳述式。 最後，當資料儲存在陣列中，通常都是螢幕資料的情況時，應用程式可以繫結所有資料列的單一呼叫之特定資料行中**SQLBindParameter**並執行單一陳述式來加以更新。  
  
 不幸的是，不多的資料來源都支援參數陣列。 不過，驅動程式可以執行一次的參數值的每一組 SQL 陳述式來模擬參數陣列。 這可能會造成速度增加，因為驅動程式可以接著準備計劃要執行一次針對每個參數集的陳述式。 它也可能會導致更簡單的應用程式程式碼。  
  
 此章節包含下列主題。  
  
-   [繫結參數陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
