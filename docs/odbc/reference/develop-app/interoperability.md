---
title: 互通性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 434b27bffe3b32aa9fa0c5c6fd3a7100e8c7ea8d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138858"
---
# <a name="interoperability"></a>互通性
*互通性*是指單一應用程式使用許多不同 dbms 操作的能力。 撰寫一般、互通的應用程式的需求，是導致 ODBC 開發的其中一個主要因素。 不過，互通性不是簡單的路徑，而是從「無法互通」到「完全互通」。 路徑有許多分支，而且每個都需要在功能、速度、程式碼複雜性和開發時間之間進行取捨。  
  
 撰寫可互通的應用程式的流程會遵循幾個步驟：  
  
1.  決定應用程式是否會使用 ODBC。  
  
2.  選擇互通性層級，並決定需要哪些取捨才能達到該層級。  
  
3.  撰寫可互通的程式碼，並盡可能完整地測試。  
  
 請注意，互通性主要是應用程式寫入器的網域。 驅動程式是設計用來處理單一 DBMS，而根據定義，它們無法互通。 它們會透過單一 DBMS 正確地執行和公開 ODBC，以在互通性中扮演角色。  
  
 此章節包含下列主題。  
  
-   [答案是 ODBC 嗎？](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [選擇互通性層級](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [判斷目標 DBMS 和驅動程式](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [考慮要使用的資料庫功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [產品週期的長度](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [撰寫可互通的應用程式](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [測試可互通的應用程式](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
