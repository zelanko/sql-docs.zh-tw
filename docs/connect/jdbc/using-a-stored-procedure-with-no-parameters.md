---
title: "使用不含任何參數的預存程序 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 19e9377f7ac42f7999ecc507a3a8aae7cbda8fc4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>使用沒有參數的預存程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  最簡單的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可以呼叫的預存程序是一個不含任何參數並且傳回單一結果集。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別，您可以使用來呼叫此種預存程序並處理其傳回的資料。  
  
 當您使用 JDBC 驅動程式呼叫不含參數的預存程序時，您必須使用`call`SQL 逸出序列。 語法`call`不含任何參數的逸出序列如下所示：  
  
 `{call procedure-name}`  
  
> [!NOTE]  
>  如需 SQL 逸出序列的詳細資訊，請參閱[使用 SQL 逸出序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 例如，建立下列預存程序中的[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫：  
  
```  
CREATE PROCEDURE GetContactFormalNames   
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName   
   FROM Person.Contact  
END  
```  
  
 此預存程序會傳回包含一個資料資料行的單一結果集，亦即 Person.Contact 資料表中前十位連絡人的職稱、名字與姓氏的組合。  
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式，而[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法用來呼叫 GetContactFormalNames 預存程序。  
  
```  
public static void executeSprocNoParams(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
  
      while (rs.next()) {  
         System.out.println(rs.getString("FormalName"));  
      }  
      rs.close();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>請參閱＜  
 [搭配使用陳述式與預存程序](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
