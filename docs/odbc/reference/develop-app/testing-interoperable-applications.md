---
title: 測試互通的應用程式 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1d43c7aad2501591c497475f6c250ac33712aa7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307739"
---
# <a name="testing-interoperable-applications"></a>測試可互通的應用程式
測試互通的應用程式最理想，因為新的驅動程式會持續出現在市場上，因此不可能最糟。 不過，可能會有合理的測試程度。 具有有限或低互通性的應用程式只需要針對它們保證支援的驅動程式進行測試。 不過，這些驅動程式必須經過完整測試。  
  
 非常互通的應用程式幾乎無法針對所有驅動程式進行測試。 大部分的應用程式開發人員最棒的就是針對少量的驅動程式進行完整測試，並 cursorily 更多。 經過測試的驅動程式應該包含最熱門的驅動程式，以用於應用程式市場中最受歡迎的 Dbms;如果市場涵蓋所有 Dbms，則應該測試桌上型電腦和伺服器 Dbms 的驅動程式。  
  
 測試 ODBC 應用程式的其中一個問題是涉及的元件數目：應用程式本身、驅動程式管理員、驅動程式、DBMS，以及可能的網路軟體或閘道。 應用程式可以透過**SQLGetDiagField**和**SQLGetDiagRec**張貼 ODBC 函式所傳回的錯誤訊息，讓您更容易追蹤錯誤。 這些訊息會識別發生錯誤的製造商和元件。 如需詳細資訊，請參閱[診斷](../../../odbc/reference/develop-app/diagnostics.md)。
