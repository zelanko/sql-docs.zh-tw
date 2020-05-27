---
title: 搭配預存程序使用陳述式 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7fe07352ff1bcda9dd3ff3e77a6b879e592235a6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "69025858"
---
# <a name="using-statements-with-stored-procedures"></a>搭配預存程序使用陳述式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

預存程序是資料庫程序，類似其他程式設計語言中的程序，包含在資料庫本身以內。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或使用 Common Language Runtime (CLR) 和其中一種 Visual Studio 程式設計語言 (如 Visual Basic 或 C#) 來建立預存程序。 一般而言，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序可執行下列動作：  
  
- 接受輸入參數，並以輸出參數的形式將多個數值傳回呼叫程序或批次處理。  
  
- 包含可在資料庫中執行作業的程式陳述式，包括呼叫其他程序。  
  
- 將狀態值傳回呼叫程序或批次處理，以指示成功或失敗 (及失敗原因)。  
  
> [!NOTE]  
> 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書中的＜了解預存程序＞。  
  
為了使用預存程序來處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別。 要使用哪一個類別視預存程序是否需要 IN (輸入) 或 OUT (輸出) 參數而定。 如果預存程序不需要 IN 或 OUT 參數，您可以使用 SQLServerStatement 類別；如果會多次呼叫預存程序，或只需要 IN 參數，則您可以使用 SQLServerPreparedStatement 類別。 如果預存程序需要 IN 與 OUT 參數，您應該使用 SQLServerCallableStatement 類別。 只有在預存程序需要 OUT 參數時，您才需要額外使用 SQLServerCallableStatement 類別。  
  
> [!NOTE]  
> 預存程序也可以傳回更新計數和多個結果集。 如需詳細資訊，請參閱[搭配更新計數使用預存程序](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)與[使用多個結果集](../../connect/jdbc/using-multiple-result-sets.md)。  
  
當使用 JDBC 驅動程式呼叫具有參數的預存程序時，您必須使用 `call` SQL 逸出序列與 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 方法搭配。 `call` 逸出序列的完整語法如下：  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
> 如需 `call` 與其他 SQL 逸出序列的詳細資訊，請參閱[使用 SQL 逸出序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
本節的主題描述您可以使用 JDBC 驅動程式和 `call` SQL 逸出序列來呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序的方式。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[使用不含參數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|描述如何使用 JDBC 驅動程式來執行不包含輸入或輸出參數的預存程序。|  
|[使用含輸入參數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|描述如何使用 JDBC 驅動程式來執行包含輸入參數的預存程序。|  
|[使用含輸出參數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|描述如何使用 JDBC 驅動程式來執行包含輸出參數的預存程序。|  
|[使用含傳回狀態的預存程序](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|描述如何使用 JDBC 驅動程式來執行包含傳回狀態值的預存程序。|  
|[使用含更新計數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|描述如何使用 JDBC 驅動程式來執行傳回更新計數的預存程序。|  
  
## <a name="see-also"></a>另請參閱

[搭配 JDBC 驅動程式使用陳述式](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
