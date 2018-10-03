---
title: 使用含有輸出參數的預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea98438694963986c31f0dbb7dddecfb5caa9da6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610826"
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>使用含有輸出參數的預存程序

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

您可以呼叫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序是會傳回一或多個 OUT 參數的預存程序，預存程序會使用這些參數將資料傳回給呼叫端應用程式。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 類別，您可以使用此類別呼叫這類型的預存程序並處理其傳回的資料。

使用 JDBC 驅動程式呼叫這類型的預存程序時，必須搭配使用 `call` SQL 逸出序列與 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 方法。 含有 OUT 參數之 `call` 逸出序列的語法如下：

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> 如需有關 SQL 逸出序列的詳細資訊，請參閱[使用 SQL 逸出序列](../../connect/jdbc/using-sql-escape-sequences.md)。

建構 `call` 逸出序列時，請使用 ? (問號) 字元來指定 IN 參數。 此字元會充當預留位置，代表將從預存程序傳回的參數值。 若要指定 OUT 參數的值，在執行預存程序之前，您必須使用 SQLServerCallableStatement 類別的 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 方法來指定每個參數的資料類型。

您在 registerOutParameter 方法中指定給 OUT 參數的值，必須是 java.sql.Types 包含的其中一個 JDBC 資料類型，然後該資料類型會對應到其中一個原生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 如需 JDBC 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型，請參閱[了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)。

當您將值傳遞到 OUT 參數的 registerOutParameter 方法時，不只要指定用於參數的資料類型，還要指定參數在預存程序中的序數位置或名稱。 比方說，如果預存程序包含單一 OUT 參數，則其序數值為 1；如果預存程序包含兩個參數，則第一個序數值為 1，第二個序數值為 2。

> [!NOTE]  
> JDBC 驅動程式不支援使用 CURSOR、SQLVARIANT、TABLE 及 TIMESTAMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型作為 OUT 參數。

例如，在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫中建立下列預存程序：

```sql
CREATE PROCEDURE GetImmediateManager  
   @employeeID INT,  
   @managerID INT OUTPUT  
AS  
BEGIN  
   SELECT @managerID = ManagerID
   FROM HumanResources.Employee
   WHERE EmployeeID = @employeeID  
END
```

此預存程序傳回單一 OUT 參數 (managerID)，它是一個整數，是以指定的 IN 參數 (employeeID) 為基礎，這個 IN 參數也是一個整數。 在 OUT 參數中傳回的值是 ManagerID，它是以 HumanResources.Employee 資料表包含的 EmployeeID 為基礎。

在下列範例中，連至 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的開啟連線會傳遞至函式，並使用 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法來呼叫 GetImmediateManager 預存程序：

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");) {  
        cstmt.setInt(1, 5);  
        cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt(2));  
    }  
}
```

這個範例會使用序數位置來識別參數。 或者，您可以使用參數的名稱而非參數的序數位置來識別該參數。 下列程式碼範例會修改上一個範例來示範如何在 Java 應用程式中使用指名參數。 請注意，參數名稱會為對應到預存程序定義中的參數名稱：

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}"); ) {  
        cstmt.setInt("employeeID", 5);  
        cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
    }  
}
```

> [!NOTE]  
> 這些範例會使用 SQLServerCallableStatement 類別的 execute 方法來執行預存程序。 會使用這個是因為預存程序並不同時傳回結果集。 如果它已傳回結果集，則會使用 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法。

預存程序可以傳回更新計數和多個結果集。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 遵循 JDBC 3.0 規格，其中說明在擷取 OUT 參數前，應該擷取多個結果集和更新計數。 也就是應用程式應該擷取所有結果集物件，並更新計數，然後再使用 CallableStatement.getter 方法擷取 OUT 參數。 否則，在擷取 OUT 參數時，將會遺失尚未擷取的 ResultSet 物件和更新計數。 如需更新計數的詳細資訊和多個結果集，請參閱[使用更新計數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)並[使用多個結果集](../../connect/jdbc/using-multiple-result-sets.md)。

## <a name="see-also"></a>另請參閱

[搭配使用陳述式與預存程序](../../connect/jdbc/using-statements-with-stored-procedures.md)
