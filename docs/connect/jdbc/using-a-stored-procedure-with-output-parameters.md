---
title: 使用預存程序輸出參數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5199b4d83b0c565015e98ab862366e9d1a53718a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852003"
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>使用含有輸出參數的預存程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可以呼叫的預存程序會傳回一或多個 OUT 參數，參數的預存程序用來傳回資料傳回到呼叫應用程式。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別，您可以使用來呼叫此種預存程序並處理其傳回的資料。  
  
 當您使用 JDBC 驅動程式呼叫此種預存程序時，您必須使用`call`SQL 逸出序列與[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。 語法`call`含有 OUT 參數的逸出序列如下所示：  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  如需 SQL 逸出序列的詳細資訊，請參閱[使用 SQL 逸出序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 當您建構`call`逸出序列，使用指定 OUT 參數？ (問號) 字元來指定 IN 參數。 此字元會充當預留位置，代表將從預存程序傳回的參數值。 若要指定 OUT 參數的值，您必須指定每個參數的資料類型使用[registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) SQLServerCallableStatement 類別，然後再執行預存程序的方法。  
  
 您指定的 registerOutParameter 方法中的 OUT 參數必須是 java.sql.Types，依序對應至其中一個原生包含 JDBC 資料類型的其中一個值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。 如需 JDBC 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型，請參閱[了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)。  
  
 當您將值傳遞至為 OUT 參數的 registerOutParameter 方法時，您必須指定不僅要用於參數，但也參數的序數位置或預存程序的參數名稱的資料型別。 比方說，如果預存程序包含單一 OUT 參數，則其序數值為 1；如果預存程序包含兩個參數，則第一個序數值為 1，第二個序數值為 2。  
  
> [!NOTE]  
>  JDBC 驅動程式不支援使用 CURSOR、 SQLVARIANT、 資料表和時間戳記[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型做為 OUT 參數。  
  
 例如，建立下列預存程序中的[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫：  
  
```  
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
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式，而[執行](../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法用來呼叫 GetImmediateManager 預存程序：  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt(1, 5);  
      cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt(2));  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
 這個範例會使用序數位置來識別參數。 或者，您可以使用參數的名稱而非參數的序數位置來識別該參數。 下列程式碼範例會修改上一個範例來示範如何在 Java 應用程式中使用指名參數。 請注意，參數名稱會為對應到預存程序定義中的參數名稱：  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt("employeeID", 5);  
      cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
      cstmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
```  
  
 }  
  
> [!NOTE]  
>  這些範例使用 SQLServerCallableStatement 類別的 execute 方法來執行預存程序。 會使用這個是因為預存程序並不同時傳回結果集。 如果有， [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法就會使用。  
  
 預存程序可以傳回更新計數和多個結果集。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]遵循 JDBC 3.0 規格，其中說明，多個結果集和更新計數應該擷取之前擷取 OUT 參數。 也就是應用程式應該擷取所有結果集物件，並更新計數，然後再使用 CallableStatement.getter 方法擷取 OUT 參數。 否則，當擷取 OUT 參數不已擷取的更新計數與結果集物件將會遺失。 如需更新計數的詳細資訊和多個結果集，請參閱[使用更新計數的預存程序](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)和[使用多個結果集](../../connect/jdbc/using-multiple-result-sets.md)。  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與預存程序](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
