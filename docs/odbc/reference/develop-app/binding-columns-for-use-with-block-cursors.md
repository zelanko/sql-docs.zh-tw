---
title: "資料行繫結區塊資料指標搭配 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4fcc0221bcf4a3555052c9562dca830e6e48f84a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="binding-columns-for-use-with-block-cursors"></a>繫結區塊資料指標搭配使用的資料行
區塊資料指標會傳回多個資料列，因為它們使用的應用程式必須繫結變數的陣列，每個資料行，而不是單一的變數。 這些陣列統稱為*緩衝區資料列集*。 以下是繫結的兩種樣式：  
  
-   將陣列繫結至每個資料行。 這稱為*資料行取向的繫結*因為每個資料結構 （陣列） 含有單一資料行的資料。  
  
-   定義包含整個資料列的資料，並將這些結構的陣列的繫結的結構。 這稱為*資料列取向的繫結*因為每個資料結構，包含單一資料列的資料。  
  
 因為當應用程式會將單一變數繫結至資料行，它會呼叫**SQLBindCol**繫結至資料行的陣列。 唯一的差別是傳遞的位址是陣列位址，而非單一的變數位址。 應用程式設定 SQL_BIND_BY_COLUMN 陳述式屬性，以指定是否使用資料行取向或資料列取向的繫結。 是否要使用資料行取向或資料列取向的繫結就是主要的應用程式喜好設定。 資料列取向繫結可能會更密切地對應至資料的應用程式的配置，在此情況下，它會提供更佳的效能。  
  
 此章節包含下列主題。  
  
-   [資料行取向的繫結](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [資料列取向的繫結](../../../odbc/reference/develop-app/row-wise-binding.md)
