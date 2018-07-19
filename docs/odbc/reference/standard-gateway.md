---
title: 標準的閘道 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6bcff520d89d9f188292f8d30632a9e05e358efa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915683"
---
# <a name="standard-gateway"></a>標準的閘道
A*閘道*是一種會使看起來像是另一個 DBMS 的軟體。 也就是說，閘道可接受的程式設計介面、 SQL 文法資料流的單一 DBMS 的通訊協定，並將它轉譯程式設計介面，也就是 SQL 文法和資料流通訊協定的隱藏 DBMS。 例如，若要使用 Microsoft® SQL Server 撰寫的應用程式也可以存取 DB2 資料透過微 Decisionware DB2 閘道;這項產品會導致 DB2 看起來像是 SQL Server。 當使用閘道時，必須是針對每個目標資料庫撰寫不同的閘道。  
  
 雖然閘道都受到 Dbms 之間的架構差異而定，它們是標準化的候選目標。 不過，如果所有 Dbms 標準化的程式設計介面，SQL 文法和資料流通訊協定的單一 DBMS，其 DBMS 是被選為標準嗎？ 當然不 DBMS 廠商很同意標準化競爭對手的產品。 如果開發的標準程式設計介面，SQL 文法和資料流通訊協定，需要進行任何閘道。
