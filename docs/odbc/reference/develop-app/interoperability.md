---
description: 互通性
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a404ee6de56cbd8b5605eca640fdf0e065f16d79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476610"
---
# <a name="interoperability"></a>互通性
*互通性* 是指單一應用程式使用許多不同 dbms 來操作的能力。 撰寫泛型、互通的應用程式的需求，是導致 ODBC 開發的其中一個主要因素。 但是，互通性並非簡單的路徑，而是從「不可互通」到「完全互通」。 路徑有許多分支，而且每個分支都需要功能、速度、程式碼複雜性和開發時間之間的取捨。  
  
 撰寫可互通的應用程式的程式會遵循幾個步驟：  
  
1.  決定應用程式是否會使用 ODBC。  
  
2.  選擇互通性層級，並決定達到該層級所需的取捨。  
  
3.  撰寫可互通的程式碼，並盡可能完整地進行測試。  
  
 請注意，互通性主要是應用程式寫入器的領域。 驅動程式是設計用來搭配單一 DBMS 運作，而且依定義無法互通。 它們藉由在單一 DBMS 上正確執行和公開 ODBC，來扮演互通性的角色。  
  
 此章節包含下列主題。  
  
-   [答案是 ODBC 嗎？](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [選擇互通性層級](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [判斷目標 DBMS 和驅動程式](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [考慮要使用的資料庫功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [產品週期的長度](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [撰寫可互通的應用程式](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [測試可互通的應用程式](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
