---
title: "互通性 |Microsoft 文件"
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
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a96949b4ca739e382a547769f496576bf13db8b7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="interoperability"></a>互通性
*互通性*是對操作上有許多不同的 Dbms 單一應用程式的能力。 需要撰寫泛型、 可互通的應用程式是一種主要的因素，導致 ODBC 的開發。 不過，互通性並不是簡單的路徑，接著再從 「 不具互通性 」 到 「 完全互通。 」 路徑有多個分支，而且每個需要的功能、 速度、 程式碼複雜度和開發時間之間的取捨。  
  
 撰寫可互通的應用程式的程序會遵循幾個步驟：  
  
1.  決定應用程式是否會使用 ODBC。  
  
2.  選擇互通性，並決定哪些取捨會到達該層級需要的層的級。  
  
3.  撰寫可互通的程式碼，並盡可能完整測試。  
  
 請注意互通性是主要的應用程式寫入器的網域。 驅動程式設計來搭配單一 DBMS，並根據定義，並不互通。 它們正確地實作及透過單一的 DBMS 公開 ODBC，互通性中扮演的角色。  
  
 此章節包含下列主題。  
  
-   [答案是 ODBC？](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [選擇互通性層的級](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [判斷目標 Dbms 和驅動程式](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [考慮要使用的資料庫功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [在產品週期的長度](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [撰寫可互通的應用程式](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [測試可互通的應用程式](../../../odbc/reference/develop-app/testing-interoperable-applications.md)

