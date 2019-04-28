---
title: 資料行繫結區塊資料指標用於 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0ed819643e7ea818fc17c0fa317473afc8f5ca3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007863"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>繫結資料行以搭配使用區塊資料指標
因為區塊資料指標會傳回多個資料列，使用它們的應用程式都必須繫結的變數的陣列設定，而不是單一的變數的每個資料行。 這些陣列通稱為*資料列集緩衝區*。 以下是繫結的兩種樣式：  
  
-   將陣列繫結至每個資料行。 這就叫做*資料行取向的繫結*因為每個資料結構 （陣列） 包含單一資料行的資料。  
  
-   定義的結構來保存整個資料列的資料，並將這些結構的陣列繫結。 這就叫做*資料列取向的繫結*因為每個資料結構包含單一資料列的資料。  
  
 因為當應用程式會將單一的變數繫結至資料行，它會呼叫**SQLBindCol**繫結至資料行的陣列。 唯一的差別是傳遞的位址陣列位址，而非單一的變數位址。 應用程式設定 SQL_BIND_BY_COLUMN 陳述式屬性，指定是否使用資料行取向或資料列取向的繫結。 是否要使用資料行取向或資料列取向的繫結就是大部分的應用程式喜好設定。 資料列取向繫結可能會更緊密對應至資料的應用程式的配置，在此情況下，它會提供更佳的效能。  
  
 此章節包含下列主題。  
  
-   [資料行取向的繫結](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [資料列取向的繫結](../../../odbc/reference/develop-app/row-wise-binding.md)
