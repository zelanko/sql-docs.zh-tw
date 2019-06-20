---
title: 以 DBMS 為基礎的驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc35f7bceff2d9e92b70448040bb602117b76c84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186297"
---
# <a name="dbms-based-drivers"></a>以 DBMS 為基礎的驅動程式
以 DBMS 為基礎的驅動程式可搭配 Oracle 或 SQL Server 等提供獨立的資料庫引擎的驅動程式使用的資料來源。 這些驅動程式透過獨立的引擎，來存取實體的資料也就是他們提交 SQL 陳述式，並從引擎中擷取結果。  
  
 以 DBMS 為基礎的驅動程式會使用現有的資料庫引擎，因為它們是通常是容易撰寫比檔案為基礎的驅動程式。 雖然以 DBMS 為基礎的驅動程式可以輕鬆地實作轉譯成原生 API 呼叫的 ODBC 呼叫，這會導致較慢的驅動程式。 若要實作以 DBMS 為基礎的驅動程式更好的方法是使用基礎資料流通訊協定，這通常是原生 API 的作用。 比方說，SQL Server 驅動程式應該使用的 TDS （資料流通訊協定適用於 SQL Server），而不是資料程式庫 (適用於 SQL Server 的原生 API)。 此規則的例外狀況時，ODBC 是原生 API。 比方說，Watcom SQL 是一個獨立的引擎，位於與應用程式相同的電腦上，而且會直接當做驅動程式載入。  
  
 以 DBMS 為基礎的驅動程式做為用戶端/伺服器組態中的用戶端資料來源會作為伺服器。 在大部分情況下，用戶端 （驅動程式） 和伺服器 （資料來源） 位於不同的電腦，雖然兩者都可能位在相同的電腦，執行多工作業的作業系統上。 第三個可能的原因是*閘道，* 這位於驅動程式和資料來源之間。 閘道是軟體的一種會導致不同的 DBMS，看起來像是另一個。 例如，若要使用 SQL Server 撰寫的應用程式也可以存取 DB2 資料透過 Micro Decisionware DB2 閘道;這項產品會導致 DB2，以便看起來像 SQL Server。  
  
 下圖顯示三種不同的設定，以 DBMS 為基礎的驅動程式。 在第一個組態中，驅動程式和資料來源位於同一部電腦上。 在第二個，驅動程式和資料來源位於不同的電腦上。 在第三，驅動程式和資料來源位於不同機器上，並位於它們位於尚未另一部電腦之間的閘道。  
  
 ![用於 DBMS 的三個組態&#45;架構的驅動程式](../../odbc/reference/media/pr07.gif "pr07")
