---
title: 使用 SQL 陳述式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5fb555b3731f9afc5296f7f558bb7a4b58b5b6bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694616"
---
# <a name="using-statements-with-sql"></a>使用 SQL 陳述式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 及內嵌 SQL 陳述式來處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料時，有不同的類別可供您使用。 使用哪一種類別視您想要執行的 SQL 陳述式類型而定。  
  
如果您的 SQL 陳述式不含任何 IN 參數，請使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 類別，但如果它確實含有 IN 參數，則請使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 類別。  
  
> [!NOTE]  
> 如果您需要使用同時包含 IN 與 OUT 參數的 SQL 陳述式，您必須將它們實作為預存程序，並使用 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別呼叫它們。 如需使用預存程序的詳細資訊，請參閱 <<c0> [ 預存程序使用的 Using 陳述式](../../connect/jdbc/using-statements-with-stored-procedures.md)。  
  
下列各節描述在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中使用 SQL 陳述式來處理資料的不同狀況。  

## <a name="in-this-section"></a>本節內容  

| 主題                                                                                                                        | Description                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [使用不含參數的 SQL 陳述式](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | 說明如何使用沒有包含任何參數的 SQL 陳述式。   |
| [搭配使用 SQL 陳述式與參數](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | 說明如何使用包含參數的 SQL 陳述式。      |
| [使用 SQL 陳述式修改資料庫物件](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | 說明如何使用 SQL 陳述式以修改資料庫物件。   |
| [使用 SQL 陳述式修改資料](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | 說明如何使用 SQL 陳述式以修改資料庫中的資料。 |
  
## <a name="see-also"></a>另請參閱

[搭配使用陳述式與 JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
