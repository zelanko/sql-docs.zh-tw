---
title: 使用陳述式與預存程序 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2e5ff4dc6ffa18d553b0b0e3bbe0c9c3a629920
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-statements-with-stored-procedures"></a>搭配預存程序使用陳述式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  預存程序是資料庫程序，類似其他程式設計語言中的程序，包含在資料庫本身以內。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，預存程序可由使用[!INCLUDE[tsql](../../includes/tsql_md.md)]，或使用 common language runtime (CLR) 和其中一種 Visual Studio 程式設計 Visual Basic 或 C# 等語言。 一般而言，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]預存程序可以執行下列動作：  
  
-   接受輸入參數，並以輸出參數的形式將多個數值傳回呼叫程序或批次處理。  
  
-   包含可在資料庫中執行作業的程式陳述式，包括呼叫其他程序。  
  
-   將狀態值傳回呼叫程序或批次處理，以指示成功或失敗 (及失敗原因)。  
  
> [!NOTE]  
>  如需有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]預存程序，請參閱中的 < 了解預存程序 >[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]線上叢書 》。  
  
 若要使用中的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用預存程序，資料庫[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)， [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)，和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別。 要使用哪一個類別視預存程序是否需要 IN (輸入) 或 OUT (輸出) 參數而定。 如果預存程序不需要 IN 或 OUT 參數，您可以使用 SQLServerStatement 類別; 事件類別如果預存程序會呼叫多次，或只需要 IN 參數，您可以使用 SQLServerPreparedStatement 類別。 如果預存程序同時需要 IN 及 OUT 參數，您應該使用 SQLServerCallableStatement 類別。 它是只預存程序需要 OUT 參數時，您必須使用 SQLServerCallableStatement 類別的額外負荷。  
  
> [!NOTE]  
>  預存程序也可以傳回更新計數和多個結果集。 如需詳細資訊，請參閱[使用預存程序與更新計數](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)和[使用多個結果集](../../connect/jdbc/using-multiple-result-sets.md)。  
  
 當您使用 JDBC 驅動程式呼叫具有參數的預存程序時，您必須使用`call`SQL 逸出序列與[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。 完整語法`call`逸出序列如下所示：  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  如需有關`call`和其他 SQL 逸出序列，請參閱[使用 SQL 逸出序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 本節中的主題描述的方式，您可以呼叫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]預存程序，使用 JDBC 驅動程式和`call`SQL 逸出序列。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[使用沒有參數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|描述如何使用 JDBC 驅動程式來執行不包含輸入或輸出參數的預存程序。|  
|[使用含有輸入參數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|描述如何使用 JDBC 驅動程式來執行包含輸入參數的預存程序。|  
|[使用含有輸出參數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|描述如何使用 JDBC 驅動程式來執行包含輸出參數的預存程序。|  
|[使用含傳回狀態的預存程序](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|描述如何使用 JDBC 驅動程式來執行包含傳回狀態值的預存程序。|  
|[使用含更新計數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|描述如何使用 JDBC 驅動程式來執行傳回更新計數的預存程序。|  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與 JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
