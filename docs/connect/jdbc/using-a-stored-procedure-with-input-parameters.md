---
title: 使用含輸入參數的預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c84e4081b9369d504d173387c6944b06d927c9c
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026899"
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>使用含輸入參數的預存程序

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

您可以呼叫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序包含一或多個 IN 參數，這些是可以用來傳遞資料給預存程序的參數。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 類別，您可以使用此類別，呼叫此種預存程序並處理其傳回的資料。

當您使用 JDBC 驅動程式呼叫含有 IN 參數的預存程序時，必須使用 `call` SQL 逸出序列與 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 方法搭配。 含有 IN 參數之 `call` 逸出序列的語法如下：

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> 如需 SQL escape 序列的詳細資訊, 請參閱[使用 sql escape 序列](../../connect/jdbc/using-sql-escape-sequences.md)。

建構 `call` 逸出序列時，請使用 ? (問號) 字元來指定 IN 參數。 此字元會充當預留位置，代表將傳入預存程序的參數值。 若要指定參數的值, 您可以使用 SQLServerPreparedStatement 類別的其中一個 setter 方法。 您可以使用的 setter 方法是由 IN 參數的資料類型決定。

當您將值傳遞至 setter 方法時，您不但要指定將用於參數中的實際值，還要指定預存程序中參數的序數位置。 例如，當您的預存程序包含單一 IN 參數時，其序數值將會是 1。 如果預存程序包含兩個參數，則第一個序數值為 1，而第二個序數值會是 2。

如需如何呼叫包含 IN 參數的預存程序範例，請在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫中使用 uspGetEmployeeManagers 預存程序。 此預存程序接受單一輸入參數 EmployeeID，它是一個整數值，並以指定的 EmployeeID 為基礎，傳回含有員工及其經理的遞迴式清單。 呼叫此預存程序的 Java 程式碼如下：

```java
public static void executeSprocInParams(Connection con) throws SQLException {  
    try(PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}"); ) {  

        pstmt.setInt(1, 50);  
        ResultSet rs = pstmt.executeQuery();  

        while (rs.next()) {  
            System.out.println("EMPLOYEE:");  
            System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER:");  
            System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
        }  
    }
}
```

## <a name="see-also"></a>另請參閱

[搭配預存程序使用陳述式](../../connect/jdbc/using-statements-with-stored-procedures.md)
