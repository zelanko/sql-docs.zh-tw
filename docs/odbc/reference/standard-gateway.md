---
title: 標準的閘道 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c70a558b065765dd9f8c0895345959e8aa22ebfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232088"
---
# <a name="standard-gateway"></a>標準閘道
A*閘道*是一種軟體，會導致不同的 DBMS，看起來像是另一個。 也就是閘道可接受的程式設計介面、 SQL 文法，資料流通訊協定的單一 DBMS，並將它轉譯到程式設計介面，也就是 SQL 文法和資料流的隱藏 DBMS 的通訊協定。 例如，若要使用 Microsoft® SQL Server 撰寫的應用程式也可以存取 DB2 資料透過 Micro Decisionware DB2 閘道;這項產品會導致 DB2，以便看起來像 SQL Server。 當使用閘道時，必須為每個目標資料庫撰寫不同的閘道。  
  
 雖然閘道都受到 Dbms 之間的架構差異，也就是標準化的良好候選項目。 不過，如果所有 Dbms 標準化的程式設計介面，SQL 文法和資料流通訊協定單一 DBMS，其 DBMS 是被選為標準的嗎？ 當然沒有商業的 DBMS 廠商很可能同意標準化競爭對手的產品。 如果開發標準的程式設計介面、 SQL 文法和資料流通訊協定，不需要任何閘道。
