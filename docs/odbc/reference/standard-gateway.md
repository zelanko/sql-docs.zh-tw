---
title: 標準閘道 :微軟文件
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
ms.openlocfilehash: 67551845c0dd8c6a28c0c4bc1c50f54ee8232df1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280071"
---
# <a name="standard-gateway"></a>標準閘道
*閘道*是使一個 DBMS 看起來像另一個軟體。 也就是說,閘道接受單個 DBMS 的程式設計介面、SQL 語法和數據流協定,並將其轉換為隱藏 DBMS 的程式設計介面、SQL 語法和數據流協定。 例如,編寫用於使用 Microsoft ® SQL Server 的應用程式™還可以透過微決策軟體 DB2 閘道存取 DB2 資料;此產品使 DB2 看起來像 SQL 伺服器。 使用閘道時,必須為每個目標資料庫編寫不同的閘道。  
  
 儘管閘道受到 DBMS 之間體系結構差異的限制,但它們是標準化的良好候選者。 但是,如果所有 DBMS 都必須在單個 DBMS 的程式設計介面、SQL 語法和數據流協定上進行標準化,那麼選擇其 DBMS 作為標準? 當然,沒有商業 DBMS 供應商可能同意對競爭對手的產品進行標準化。 如果開發了標準程式設計介面、SQL 語法和數據流協定,則不需要閘道。
