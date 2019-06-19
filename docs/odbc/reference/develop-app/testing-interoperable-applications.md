---
title: 測試可互通的應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 509dd17efeeb982c51938d7a18fad99a2e84ba5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63148934"
---
# <a name="testing-interoperable-applications"></a>測試可互通的應用程式
測試可互通的應用程式是在最耗時的商務和最糟的情況不可能因為市場上不斷出現新的驅動程式。 不過，一定的測試可能會。 有限或低的互通性的應用程式只需要針對保證可支援這些驅動程式進行測試。 不過，它們必須是完全針對測試這些驅動程式。  
  
 高度互通的應用程式無法針對所有的驅動程式實際上並進行測試。 大部分的應用程式開發人員可執行的最佳是完全針對一小部分的驅動程式和 cursorily 更多測試。 測試驅動程式應該包含在應用程式的市場; 中最受歡迎的 Dbms 的最受歡迎的驅動程式如果市面上涵蓋所有的 Dbms，桌上型電腦和伺服器的 Dbms 的驅動程式應該經過測試。  
  
 測試 ODBC 應用程式的問題之一是所涉及的元件數目： 應用程式本身、 驅動程式管理員、 驅動程式、 DBMS，並可能是網路軟體或閘道。 應用程式可以輕鬆地追蹤錯誤，藉由公佈透過 ODBC 函數所傳回的錯誤訊息**SQLGetDiagField**並**SQLGetDiagRec**。 製造商和元件發生錯誤，找出這些訊息。 如需詳細資訊，請參閱 <<c0> [ 診斷](../../../odbc/reference/develop-app/diagnostics.md)。
