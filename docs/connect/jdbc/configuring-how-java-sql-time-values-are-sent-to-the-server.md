---
title: 設定 java.sql.Time 值傳送至伺服器的方式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e2e91550767715616599c2720c99b864363a185
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>設定 java.sql.Time 值如何傳送給伺服器
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  如果您使用 java.sql.Time 物件或 java.sql.Types.TIME JDBC 型別來設定參數時，您可以設定 java.sql.Time 值如何傳送到伺服器;為[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**時間**類型或**datetime**型別。  
  
 當您使用下列其中一個方法時，這個情況將會適用：  
  
-   [SQLServerCallableStatement.registerOutParameter （int，int）](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter （int，int，int）](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 您可以設定 java.sql.Time 值如何傳送使用**sendTimeAsDatetime**連接屬性。 如需詳細資訊，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 您可以透過程式設計方式修改值**sendTimeAsDatetime**連接屬性[SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 新版[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]早於[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]不支援**時間**資料類型，所以通常使用 java.sql.Time 的應用程式儲存 java.sql.Time 值儲存為**datetime**或**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
 如果您想要使用**datetime**和**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料類型使用 java.sql.Time 值時，您應該設定**sendTimeAsDatetime**連接屬性設**true**。 如果您想要使用**時間**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別時使用 java.sql.Time 值時，您應該設定**sendTimeAsDatetime**連接屬性設**false**.  
  
 請注意，當將 java.sql.Time 值傳送參數資料類型同時可以儲存日期，該預設日期會因為 java.sql.Time 值會以傳送而有所不同**datetime** (1/1/1970) 或**時間**(1/1/1900) 值。 如需有關資料轉換時將資料傳送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱[使用日期和時間資料](http://go.microsoft.com/fwlink/?LinkID=145211)。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]JDBC Driver 3.0 中， **sendTimeAsDatetime**預設為 true。 在未來版本中， **sendTimeAsDatetime**連接屬性可能會依預設設定為 false。  
  
 若要確保您的應用程式仍可繼續正常運作的預設值為何**sendTimeAsDatetime**連接屬性，您可以：  
  
-   處理時使用 java.sql.Time**時間**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
-   處理時使用 java.sql.Timestamp **datetime**， **smalldatetime**，和**datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料型別。  
  
請注意該 sendTimeAsDatetime 必須加密的資料行，則為 false，因為加密資料行不支援時間轉換成日期時間。 從 Microsoft JDBC Driver 6.0 for SQL Server，SQLServerConnection 類別有下列兩個方法來設定/取得 sendTimeAsDatetime 屬性的值。

```
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
