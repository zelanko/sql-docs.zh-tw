---
title: 使用 SQL 陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac74ec1c202341d6de099d97e2b7c719c2f72d27
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-statements-with-sql"></a>使用 SQL 陳述式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當您使用中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]及內嵌 SQL 陳述式，您可以使用的不同類別。 使用哪一種類別視您想要執行的 SQL 陳述式類型而定。  
  
 如果您的 SQL 陳述式不含任何 IN 參數，使用[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別，但如果它確實含有 IN 參數，使用[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)類別。  
  
> [!NOTE]  
>  如果您需要使用 SQL 陳述式同時包含 IN 與 OUT 參數，您必須它們實作為預存程序，並使用呼叫它們[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別。 如需有關如何使用預存程序的詳細資訊，請參閱[使用陳述式與預存程序](../../connect/jdbc/using-statements-with-stored-procedures.md)。  
  
 下列章節說明使用中的資料之不同案例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫使用 SQL 陳述式。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[使用不含參數的 SQL 陳述式](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)|說明如何使用沒有包含任何參數的 SQL 陳述式。|  
|[搭配使用 SQL 陳述式與參數](../../connect/jdbc/using-an-sql-statement-with-parameters.md)|說明如何使用包含參數的 SQL 陳述式。|  
|[使用 SQL 陳述式修改資料庫物件](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md)|說明如何使用 SQL 陳述式以修改資料庫物件。|  
|[使用 SQL 陳述式修改資料](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)|說明如何使用 SQL 陳述式以修改資料庫中的資料。|  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與 JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
