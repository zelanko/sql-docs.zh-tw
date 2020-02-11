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
ms.openlocfilehash: fcd2221d9a0bb9cba42745901e5f00a6f8c8415e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111253"
---
# <a name="dbms-based-drivers"></a>以 DBMS 為基礎的驅動程式
以 DBMS 為基礎的驅動程式會與資料來源（例如 Oracle 或 SQL Server）搭配使用，以提供獨立的資料庫引擎供驅動程式使用。 這些驅動程式會透過獨立引擎存取實體資料;也就是說，它們會將 SQL 語句提交至，並從引擎取得結果。  
  
 因為 DBMS 型驅動程式使用現有的資料庫引擎，所以通常比以檔案為基礎的驅動程式更容易撰寫。 雖然以 DBMS 為基礎的驅動程式可以藉由將 ODBC 呼叫轉譯為原生 API 呼叫來輕鬆地執行，但這會導致驅動程式變慢。 採用以 DBMS 為基礎的驅動程式的更好方法是使用基礎資料流程通訊協定，這通常是原生 API 的功能。 例如，SQL Server 驅動程式應該使用 TDS （適用于 SQL Server 的資料流程通訊協定），而不是 DB 程式庫（適用于 SQL Server 的原生 API）。 此規則的例外狀況是當 ODBC 是原生 API 時。 例如，Watcom SQL 是獨立的引擎，其位於與應用程式相同的電腦上，並直接載入為驅動程式。  
  
 以 DBMS 為基礎的驅動程式會作為用戶端/伺服器設定中的用戶端，其中資料來源會當做伺服器。 在大部分情況下，用戶端（驅動程式）和伺服器（資料來源）位於不同的電腦上，雖然兩者都可以位於執行多工作業系統的同一部電腦上。 第三種可能性是位於驅動程式與資料來源之間的*閘道*。 閘道是一種軟體，讓一個 DBMS 看起來像另一個。 例如，使用 SQL Server 撰寫的應用程式也可以透過微 Decisionware DB2 閘道存取 DB2 資料;這種產品會使 DB2 看起來像 SQL Server。  
  
 下圖顯示以 DBMS 為基礎的驅動程式的三個不同設定。 在第一個設定中，驅動程式和資料來源位於相同的電腦上。 在第二個中，驅動程式和資料來源位於不同的電腦上。 在第三個中，驅動程式和資料來源位於不同的電腦上，而閘道則位於另一部電腦上。  
  
 ![以 DBMS&#45;為基礎之驅動程式的三個設定](../../odbc/reference/media/pr07.gif "pr07")
