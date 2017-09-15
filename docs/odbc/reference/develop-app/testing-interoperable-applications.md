---
title: "測試可互通的應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d36c443cb6bc4a189006a3d63e90deead3f11e66
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="testing-interoperable-applications"></a>測試可互通的應用程式
測試可互通的應用程式是使用最佳耗時業務和最糟的情況不可能因為市場上持續出現新的驅動程式。 不過，有合理的程度的測試可能是。 有限或過低的互通性的應用程式只需要針對保證可支援這些驅動程式進行測試。 不過，它們必須經過完整測試對這些驅動程式。  
  
 無法針對所有的驅動程式實際上測試具備高度互通性的應用程式。 可以執行大部分的應用程式開發人員的最佳方式為測試它們，完全是針對少數的驅動程式和 cursorily 更多。 已測試的驅動程式應該包含應用程式的市場; 最受歡迎的 Dbms 最受歡迎的驅動程式如果市場涵蓋所有 Dbms，應該經過測試的桌上型電腦和伺服器 Dbms 驅動程式。  
  
 測試 ODBC 應用程式問題的其中一個是相關的元件數目： 應用程式本身、 驅動程式管理員、 驅動程式、 DBMS，和可能的網路軟體或閘道。 應用程式可以更輕鬆地追蹤錯誤，藉由公佈透過 ODBC 函數所傳回的錯誤訊息**SQLGetDiagField**和**SQLGetDiagRec**。 這些訊息會識別的製造商和發生錯誤的元件。 如需詳細資訊，請參閱[診斷](../../../odbc/reference/develop-app/diagnostics.md)。
