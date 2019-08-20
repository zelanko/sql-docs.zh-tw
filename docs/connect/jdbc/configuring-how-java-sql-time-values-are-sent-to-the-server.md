---
title: 設定 java.sql.Time 值如何傳送給伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fe6969d51834d0798a530b9cc9926af1b27fec2
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028232"
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>設定 java.sql.Time 值如何傳送給伺服器
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  如果您使用 java.sql.Time 物件或 java.sql.Types.TIME JDBC 類型來設定參數，則可以設定 java.sql.Time 值如何當成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **time** 類型或 **datetime** 類型傳送給伺服器。  
  
 當您使用下列其中一個方法時，這個情況將會適用：  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 您可以設定 java.sql.Time 值如何使用 **sendTimeAsDatetime** 連線屬性來傳送。 如需詳細資訊，請參閱[設定連線屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 您可以使用程式設計方式，透過 [SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 修改 **sendTimeAsDatetime** 連線屬性的值。  
  
 早于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   的版本不支援 time 資料類型, 因此使用 sql-dmo 的應用程式通常會將 java. time 值儲存為 datetime 或 Smalldatetime 資料類型。 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]  
  
 如果您想要在使用**sendTimeAsDatetime**連接屬性時, 使用**datetime**和**Smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型, 您應該將此設定為**true**。 如果您想要在使用 sendTimeAsDatetime 連接屬性時使用**time** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型, 您應該將 [  ] 連接屬性設定為 [ **false**]。  
  
 請注意，將 java.sql.Time 值傳送給資料類型同時可以儲存日期的參數時，該預設日期會因為 java.sql.Time 值傳送為 **datetime** (1/1/1970) 或 **time** (1/1/1900) 值而有所不同。 如需將資料傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時之資料轉換的詳細資訊，請參閱[使用日期和時間資料](https://go.microsoft.com/fwlink/?LinkID=145211)。  
  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中, **sendTimeAsDatetime**預設為 true。 在未來的版本中，**sendTimeAsDatetime** 連線屬性可能會預設為 false。  
  
 若要確保應用程式能夠依照預期的形式繼續運作，而不論 **sendTimeAsDatetime** 連線屬性的預設值為何，您可以：  
  
-   在處理 **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型時使用 java.sql.Time。  
  
-   當使用**datetime**、 **Smalldatetime**和**datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型時, 請使用 .sql. Timestamp。  
  
加密資料行的 SendTimeAsDatetime 必須是 false, 因為加密資料行不支援從 time 轉換成 datetime。 從 Microsoft JDBC Driver 6.0 for SQL Server 開始, SQLServerConnection 類別有下列兩種方法可設定/取得 sendTimeAsDatetime 屬性的值。

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>另請參閱
 [了解 JDBC 驅動程式資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
