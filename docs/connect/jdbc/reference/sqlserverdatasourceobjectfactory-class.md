---
title: SQLServerDataSourceObjectFactory 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 135dad379d0642059af19060b9df27baec0e3e24
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615187"
---
# <a name="sqlserverdatasourceobjectfactory-class"></a>SQLServerDataSourceObjectFactory 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表可具體化來自 Java Naming and Directory Interface (JNDI) 之資料來源的物件 Factory。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.lang.Object  
  
 **實作：** javax.naming.spi.ObjectFactory  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerDataSourceObjectFactory  
```  
  
## <a name="remarks"></a>Remarks  
 所有的資料來源類別都會繼承這個方法。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會公開實作 ObjectFactory 的這個類別，當作其對可參考介面的支援。 Java 應用程式伺服器將對資料來源類別呼叫 getReference，而這將會建立從內部使用該類別名稱作為其 Class Factory 的 Reference 物件。  
  
 當 Java 應用程式伺服器具有參考物件取值 （dereference） 時，它會建立 SQLServerDataSourceObjectFactory 物件和呼叫的執行個體[getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md)方法，並在所參考的物件傳遞至擷取資料來源執行個體。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSourceObjectFactory 成員](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
