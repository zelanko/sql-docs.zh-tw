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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03479a0187c7720a595b550290a8f5ac8197fa9c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686326"
---
# <a name="arrays-of-parameter-values"></a>參數值陣列
它通常是用於將參數陣列的應用程式。 例如，使用參數和參數化的陣列**插入**陳述式中，應用程式可以一次插入的資料列數目。 有數個優點，來使用陣列。 首先，因為 （如果資料來源原生支援的參數陣列），將會傳送單一封包中的多個陳述式的資料可以降低網路流量。 第二，某些資料來源，可以執行速度比執行相同數目的個別 SQL 陳述式使用陣列的 SQL 陳述式。 最後，當資料儲存在陣列中，通常就是螢幕資料的情況，應用程式可以繫結所有資料列中的單一呼叫的特定資料行**SQLBindParameter**並執行單一陳述式來更新它們。  
  
 不幸的是，不多的資料來源都支援參數陣列。 不過，驅動程式可以模擬參數陣列執行的 SQL 陳述式，針對每一組參數值執行一次。 這可能會導致速度因為驅動程式可以接著準備計劃要執行一次針對每個參數集的陳述式。 它也可能會導致更簡單的應用程式程式碼。  
  
 此章節包含下列主題。  
  
-   [繫結參數陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
