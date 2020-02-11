---
title: 標準閘道 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8120f3cda584240b0b58ed5d6758621b18fe44d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070483"
---
# <a name="standard-gateway"></a>標準閘道
*閘道*是一種軟體，讓一個 DBMS 看起來像另一個。 也就是說，閘道會接受單一 DBMS 的程式設計介面、SQL 文法和資料流程通訊協定，並將它轉譯成隱藏 DBMS 的程式設計介面、SQL 文法和資料流程通訊協定。 例如，撰寫為使用 Microsoft® SQL Server™的應用程式也可以透過微 Decisionware DB2 閘道存取 DB2 資料;這種產品會使 DB2 看起來像 SQL Server。 使用閘道時，必須為每個目標資料庫寫入不同的閘道。  
  
 雖然閘道會受到 Dbms 間的架構差異的限制，但它們是標準化的理想候選。 不過，如果所有 Dbms 都是在單一 DBMS 的程式設計介面、SQL 文法和資料流程通訊協定上標準化，其 DBMS 會被選擇做為標準嗎？ 當然，沒有任何商業 DBMS 廠商可能同意在競爭對手的產品上標準化。 而且，如果開發了標準程式設計介面、SQL 文法和資料流程通訊協定，就不需要任何閘道。
