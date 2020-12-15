---
description: 使用陳述式參數
title: Using 語句參數 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- ODBC, parameters
- statements [ODBC], parameters
- parameter markers [ODBC]
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
ms.assetid: 2427d886-ec6c-49d7-b0b6-0d998b64cdb9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b05c7d20deb1108e5e4c7f74fffce42072ba8515
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478059"
---
# <a name="using-statement-parameters"></a>使用陳述式參數
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  參數是 SQL 陳述式內的變數，可讓 ODBC 應用程式進行以下作業：  
  
-   有效率地針對資料表中的資料行提供值。  
  
-   增強建構查詢準則時的使用者互動。  
  
-   管理 **text**、 **Ntext** 和 **image** 資料，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的 C 資料類型。  
  
 例如， **Parts** 資料表具有名為 **PartID**、 **Description** 和 **Price** 的資料行。 加入某個部分而不含參數時，需要建構如下的 SQL 陳述式：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 雖然可接受這個陳述式插入具有一組已知值的一個資料列，但是當應用程式需要插入幾個資料列時，還是有點不便。 ODBC 為了應付這個狀況，所以讓應用程式可使用參數標記取代 SQL 陳述式中的任何資料值。 這是由問號 (?) 表示。 在下列範例中，會以參數標記來取代三個資料值：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 然後會將參數標記繫結到應用程式變數。 若要插入新的資料列，應用程式只需要設定變數的值，然後再執行此陳述式。 然後驅動程式會擷取目前的變數值，再將其傳送給資料來源。 如果此陳述式執行多次，應用程式可以預備此陳述式來讓處理程序更有效率。  
  
 每一個參數標記都是根據從左到右指派給參數的序數來參考。 SQL 陳述式中最左邊參數標記的序數值為 1，下一個標記的序數值為 2，依此類推。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [繫結參數](../../relational-databases/native-client-odbc-queries/using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;執行查詢 ](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
