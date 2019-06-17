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
manager: craigg
ms.openlocfilehash: 8d5e4fbee458bec88461d3e2945a466c848d3345
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446485"
---
# <a name="interoperability"></a>互通性
*互通性*是單一的應用程式，有許多不同的 Dbms 一起運作的能力。 您不必撰寫泛型、 可互通的應用程式是其中一個連至 ODBC 的開發的主要選擇要素。 不過，互通性不是簡單的路徑，接著再從 「 不具互通性 」 到 「 完全互通。 」 路徑有多個分支，而且每個需要功能、 速度、 程式碼複雜度和開發時間之間的取捨。  
  
 撰寫可互通的應用程式的程序會遵循幾個步驟：  
  
1.  決定應用程式是否會使用 ODBC。  
  
2.  選擇互通性，並決定哪些取捨的必須觸達該層級層的級。  
  
3.  撰寫可互通的程式碼，並儘可能完全加以測試。  
  
 請注意，互通性是主要的應用程式寫入器的網域。 驅動程式設計來搭配單一 DBMS，並根據定義，不具互通性。 它們正確地實作，並透過單一的 DBMS 公開 ODBC，互通性的一部分的影響力。  
  
 此章節包含下列主題。  
  
-   [答案是 ODBC 嗎？](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [選擇互通性層級](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [判斷目標 DBMS 和驅動程式](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [考慮要使用的資料庫功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [產品週期的長度](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [撰寫可互通的應用程式](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [測試可互通的應用程式](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
