---
title: 使用含傳回狀態的預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b5b5425dcc88a3f4a2b5bc24c85ab41beb04bb48
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027116"
---
# <a name="using-a-stored-procedure-with-a-return-status"></a>使用含傳回狀態的預存程序

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

您可以呼叫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序是會傳回狀態或結果參數的預存程序。 這通常用來指出預存程序的成功或失敗。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別，您可以使用此類別，呼叫此種類的預存程序並處理其傳回的資料。

當您使用 JDBC 驅動程式來呼叫此種預存程序時，您必須使用 `call` SQL 逸出序列來搭配 [SQLServerConnection](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 類別的 [prepareCall](../../connect/jdbc/reference/sqlserverconnection-class.md) 方法。 含有傳回狀態參數之 `call` 逸出序列的語法如下：

`{[?=]call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> 如需 SQL 逸出序列的詳細資訊，請參閱[使用 SQL 逸出序列](../../connect/jdbc/using-sql-escape-sequences.md)。

當您建構 `call` 逸出序列時，請使用 ? (問號) 字元來指定 IN 參數。 此字元會充當預留位置，代表將從預存程序傳回的參數值。 若要指定傳回狀態參數的值，在執行預存程序之前，您必須使用 SQLServerCallableStatement 類別的 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 方法來指定參數的資料類型。

> [!NOTE]  
> 搭配使用 JDBC 驅動程式與 SQL Server 資料庫時，在 registerOutParameter 方法中指定給傳回狀態參數的值一律為整數，您可以使用 java.sql.Types.INTEGER 資料類型來指定此整數。

此外，當您將值傳遞至傳回狀態參數的 registerOutParameter 方法時，您不只要指定使用於參數的資料類型，還要指定參數在預存程序呼叫中的序數位置。 以傳回狀態參數而言，其序數位置一律為 1，因為它一律為預存程序呼叫中的第一個參數。 雖然 SQLServerCallableStatement 類別提供使用參數名稱表示特定參數的支援，但是您只能將參數的序數位置號碼用於傳回狀態參數。

例如，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫中建立下列預存程序：

```sql
CREATE PROCEDURE CheckContactCity  
   (@cityName CHAR(50))  
AS  
BEGIN  
   IF ((SELECT COUNT(*)  
   FROM Person.Address  
   WHERE City = @cityName) > 1)  
   RETURN 1  
ELSE  
   RETURN 0  
END  
```

此預存程序傳回狀態值 1 或 0，視 cityName 參數中指定的城市是否可在 Person.Address 資料表中找到而定。

在下列範例中，[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線會傳入至函式中，並使用 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法來呼叫 CheckContactCity 預存程序：

[!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]

## <a name="see-also"></a>另請參閱

[搭配預存程序使用陳述式](../../connect/jdbc/using-statements-with-stored-procedures.md)
