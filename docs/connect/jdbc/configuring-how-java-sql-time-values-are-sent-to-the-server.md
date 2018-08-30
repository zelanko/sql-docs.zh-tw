---
title: 設定 java.sql.Time 值如何傳送給伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
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
ms.openlocfilehash: fcb15ace351d53ed072738ea9e8978eb681294b0
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42787160"
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
  
 新版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]早於[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]不支援**時間**資料類型，所以通常使用 java.sql.Time 的應用程式儲存 java.sql.Time 值儲存為**datetime**或**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。  
  
 如果您想要使用**datetime**並**smalldatetime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型使用 java.sql.Time 值時，您應該設定**sendTimeAsDatetime**若要連接屬性 **，則為 true**。 如果您想要使用**時間**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型時使用 java.sql.Time 值時，您應該設定**sendTimeAsDatetime**連接屬性設**false**.  
  
 請注意，將 java.sql.Time 值傳送給資料類型同時可以儲存日期的參數時，該預設日期會因為 java.sql.Time 值傳送為 **datetime** (1/1/1970) 或 **time** (1/1/1900) 值而有所不同。 如需將資料傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時之資料轉換的詳細資訊，請參閱[使用日期和時間資料](http://go.microsoft.com/fwlink/?LinkID=145211)。  
  
 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC 驅動程式 3.0 中， **sendTimeAsDatetime**預設為 true。 在未來的版本中，**sendTimeAsDatetime** 連線屬性可能會預設為 false。  
  
 若要確保應用程式能夠依照預期的形式繼續運作，而不論 **sendTimeAsDatetime** 連線屬性的預設值為何，您可以：  
  
-   在處理 **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型時使用 java.sql.Time。  
  
-   處理時使用 java.sql.Timestamp **datetime**， **smalldatetime**，並**datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。  
  
SendTimeAsDatetime 必須是加密的資料行，則為 false，因為加密資料行不支援時間轉換成日期時間。 從 Microsoft JDBC Driver 6.0 for SQL Server，SQLServerConnection 類別具有下列兩個方法來設定/取得 sendTimeAsDatetime 屬性的值。

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
