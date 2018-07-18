---
title: 預存程序使用傳回狀態 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29bb95c06d86ad4d6e45002da1429f6c7d5a5c9e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853153"
---
# <a name="using-a-stored-procedure-with-a-return-status"></a>使用含傳回狀態的預存程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]可以呼叫的預存程序是會傳回狀態或結果參數。 這通常用來指出預存程序的成功或失敗。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)類別，您可以使用呼叫此種類的預存程序並處理其傳回的資料。  
  
 當您使用 JDBC 驅動程式呼叫此種預存程序時，您必須使用`call`搭配 SQL 逸出序列[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)方法[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別. 語法`call`使用傳回狀態參數的逸出序列如下所示：  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  如需 SQL 逸出序列的詳細資訊，請參閱[使用 SQL 逸出序列](../../connect/jdbc/using-sql-escape-sequences.md)。  
  
 當您建構`call`逸出序列，使用指定的傳回狀態參數？ (問號) 字元來指定 IN 參數。 此字元會充當預留位置，代表將從預存程序傳回的參數值。 若要指定傳回狀態參數的值，您必須指定參數的資料類型使用[registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) SQLServerCallableStatement 類別，再執行預存程序的方法。  
  
> [!NOTE]  
>  當使用 SQL Server 資料庫的 JDBC 驅動程式，您指定 registerOutParameter 方法中，傳回狀態參數值一律會是整數，您可以使用 java.sql.Types.INTEGER 資料類型指定。  
  
 此外，當您將值傳遞給傳回狀態參數的 registerOutParameter 方法時，您必須指定不僅要用於參數，但也在預存程序呼叫參數的序數位置的資料型別。 以傳回狀態參數而言，其序數位置一律為 1，因為它一律為預存程序呼叫中的第一個參數。 雖然 SQLServerCallableStatement 類別會提供使用參數的名稱表示特定參數的支援，但是您可以使用參數的序數位置號碼用於傳回狀態參數。  
  
 例如，建立下列預存程序中的[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫：  
  
```  
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
  
 在下列範例中，開啟連接[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫會傳遞至函式，而[執行](../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法用來呼叫 CheckContactCity 預存程序：  
  
 [!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]  
  
## <a name="see-also"></a>另請參閱  
 [搭配使用陳述式與預存程序](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
