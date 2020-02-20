---
title: SQLServerDataSourceObjectFactory 類別 | Microsoft Docs
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
ms.openlocfilehash: cf4c90644282ff420e064e7a7b5b99a93c257194
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67971386"
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
  
## <a name="remarks"></a>備註  
 所有的資料來源類別都會繼承這個方法。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會公開實作 ObjectFactory 的這個類別，當作其對可參考介面的支援。 Java 應用程式伺服器將對資料來源類別呼叫 getReference，而這將會建立從內部使用該類別名稱作為其 Class Factory 的 Reference 物件。  
  
 當 Java 應用程式伺服器必須為 Reference 物件取值 (Dereference) 時，它會建立 SQLServerDataSourceObjectFactory 物件的執行個體，然後呼叫會傳遞 Reference 物件的 [getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md) 方法，進行資料來源執行個體的擷取。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSourceObjectFactory 成員](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
