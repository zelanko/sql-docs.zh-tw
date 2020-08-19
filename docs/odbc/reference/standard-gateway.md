---
description: 標準閘道
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 687097813d01b27ac49e657f11a2b763e2ca1214
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448898"
---
# <a name="standard-gateway"></a>標準閘道
*閘道*是一種軟體，可讓一個 DBMS 看起來像另一個 DBMS。 也就是說，閘道會接受單一 DBMS 的程式設計介面、SQL 文法和資料流程通訊協定，並將其轉譯為隱藏 DBMS 的程式設計介面、SQL 文法和資料流程通訊協定。 例如，撰寫為使用 Microsoft® SQL Server™的應用程式也可以透過微 Decisionware DB2 閘道來存取 DB2 資料;此產品會使 DB2 看起來像 SQL Server。 使用閘道時，必須為每個目標資料庫撰寫不同的閘道。  
  
 雖然閘道受限於 Dbms 之間的架構差異，但它們是理想的標準化候選。 但是，如果所有 Dbms 都是針對單一 DBMS 的程式設計介面、SQL 文法和資料流程通訊協定進行標準化，則會將其 DBMS 選為標準？ 當然，任何商業 DBMS 廠商都不可能同意在競爭對手的產品上標準化。 而且，如果開發的是標準的程式設計介面、SQL 文法和資料流程通訊協定，則不需要閘道。
