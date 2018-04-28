---
title: 使用輸入參數的預存程序 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 64bf5a293cbe0f9fd9287a03084d66044a54337a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>使用含有輸入參數的預存程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可以呼叫的預存程序是指包含一或多 IN 參數，這是可用來將資料傳遞至預存程序的參數。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)類別，您可以使用呼叫此種類的預存程序並處理其傳回的資料。  
  
 當您使用 JDBC 驅動程式來呼叫預存程序參數中時，您必須使用`call`SQL 逸出序列與[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。 語法`call`含有 IN 參數的逸出序列如下所示：  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  如需 SQL 逸出序列的詳細資訊，請參閱[使用 SQL 逸出序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 當您建構`call`逸出序列，使用指定 IN 參數？ (問號) 字元來指定 IN 參數。 此字元會充當預留位置，代表將傳入預存程序的參數值。 若要指定參數的值，您可以使用 SQLServerPreparedStatement 類別的 setter 方法的其中一個。 您可以使用的 setter 方法是由 IN 參數的資料類型決定。  
  
 當您將值傳遞至 setter 方法時，您不但要指定將用於參數中的實際值，還要指定預存程序中參數的序數位置。 例如，當您的預存程序包含單一 IN 參數時，其序數值將會是 1。 如果預存程序包含兩個參數，則第一個序數值為 1，而第二個序數值會是 2。  
  
 如何呼叫包含 IN 參數的預存程序的範例，使用 uspGetEmployeeManagers 預存程序中的[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫。 此預存程序接受單一輸入參數 EmployeeID，它是一個整數值，並以指定的 EmployeeID 為基礎，傳回含有員工及其經理的遞迴式清單。 呼叫此預存程序的 Java 程式碼如下：  
  
```  
public static void executeSprocInParams(Connection con) {  
   try {  
      PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}");  
      pstmt.setInt(1, 50);  
      ResultSet rs = pstmt.executeQuery();  
  
      while (rs.next()) {  
         System.out.println("EMPLOYEE:");  
         System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
         System.out.println("MANAGER:");  
         System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
         System.out.println();  
      }  
      rs.close();  
      pstmt.close();  
   }  
  
   catch (Exception e) {  
      e.printStackTrace();  
    }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與預存程序](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
