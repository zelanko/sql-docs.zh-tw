---
title: 互操作性 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31b20a696c601ff91c591e4c717f468beca34e36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306219"
---
# <a name="interoperability"></a>互通性
*互操作性*是單個應用程式使用許多不同的 DBMS 運行的能力。 編寫通用、可互通的應用程式是導致 ODBC 開發的主要因素之一。 但是,互操作性不是從"不可互操作"到"完全可互操作"的簡單路徑。 路徑具有許多分支,每個分支都需要在功能、速度、代碼複雜性和開發時間之間進行權衡。  
  
 編寫可互通的應用程式的過程遵循幾個步驟:  
  
1.  確定應用程式是否將使用 ODBC。  
  
2.  選擇互操作性級別,並決定達到該級別所需的權衡。  
  
3.  編寫可互操作的代碼並盡可能完整地測試它。  
  
 需要注意的是,互操作性主要是應用程式編寫器的域。 驅動程式設計為使用單個 DBMS,並且根據定義,它們不可互通。 通過在單個 DBMS 上正確實現和公開 ODBC,它們在互通性方面發揮著作用。  
  
 此章節包含下列主題。  
  
-   [答案是 ODBC 嗎？](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [選擇互通性層級](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [判斷目標 DBMS 和驅動程式](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [考慮要使用的資料庫功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [產品週期的長度](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [撰寫可互通的應用程式](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [測試可互通的應用程式](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
