---
title: "DBMS 架構驅動程式 |Microsoft 文件"
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
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b806f4c887af3f1ba80ee3321820e97dd336fad
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="dbms-based-drivers"></a>DBMS 架構驅動程式
DBMS 架構驅動程式會搭配如 Oracle 或 SQL Server 提供驅動程式使用的獨立資料庫引擎的資料來源。 這些驅動程式透過獨立的引擎; 存取實體的資料也就是它們提交 SQL 陳述式，並從引擎中擷取結果。  
  
 DBMS 架構驅動程式會使用現有的資料庫引擎，因為它們是通常是容易撰寫比以檔案為基礎的驅動程式。 雖然 DBMS 架構驅動程式可以輕鬆地實作凙 ODBC 呼叫原生 API 呼叫，這會導致較慢的驅動程式。 實作 DBMS 架構驅動程式的較佳方式是使用基礎資料流通訊協定，這通常是原生應用程式開發介面的作用。 例如，SQL Server 驅動程式應該使用的 TDS （資料流適用於 SQL Server 通訊協定） 而不是資料程式庫 (適用於 SQL Server 的原生 API)。 此規則的例外狀況時，ODBC 是在原生 API。 例如，Watcom SQL 是獨立的引擎，位於應用程式相同的電腦上，而且會直接當做驅動程式載入。  
  
 DBMS 架構驅動程式做為用戶端/伺服器組態中的用戶端資料來源做為伺服器的位置。 在大部分情況下，用戶端 （驅動程式） 和伺服器 （資料來源） 位於不同機器上，雖然都是可能位在相同的電腦執行多工作業的作業系統上。 第三個可能的原因是*閘道，*這位於驅動程式與資料來源之間。 閘道器是軟體的一種會使看起來像是另一個 DBMS。 例如，若要使用 SQL Server 撰寫的應用程式也可以存取 DB2 資料透過微 Decisionware DB2 閘道;這項產品會導致 DB2 看起來像是 SQL Server。  
  
 下圖顯示三個不同的組態，DBMS 架構驅動程式。 在第一個組態，驅動程式和資料來源位於同一部電腦上。 在第二個，驅動程式和資料來源位於不同的電腦上。 在第三個，驅動程式和資料來源位於不同機器上，閘道位於其間，位於另一個的電腦上。  
  
 ![三種 DBMS 的設定 &#45; 根據的 drivers](../../odbc/reference/media/pr07.gif "pr07")
