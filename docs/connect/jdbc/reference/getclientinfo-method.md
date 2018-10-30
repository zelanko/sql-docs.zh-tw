---
title: getClientInfo 方法 （) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b06a5ced-b760-4c78-b17e-854ce95a1a5c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a89f2afa50b0ee1b83e72c05bf675d49dac662ca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757766"
---
# <a name="getclientinfo-method-"></a>getClientInfo 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取清單，此清單包含 JDBC Driver 所支援之個別用戶端資訊的名稱和最新值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.util.Properties getClientInfo()  
```  
  
## <a name="return-value"></a>傳回值  
 Properties 物件，其中包含驅動程式所支援個別用戶端資訊屬性的名稱和最新值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getClientInfo 方法是由 java.sql.Connection 介面中的 getClientInfo 方法指定。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 不支援任何用戶端資訊屬性。 如此一來，這個方法會傳回空的屬性物件。  
  
 同樣地，應用程式可以使用 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 類別的 [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 方法，擷取驅動程式所支援用戶端資訊屬性的清單。 [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 方法會傳回空的結果集。  
  
## <a name="see-also"></a>另請參閱  
 [getClientInfo 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
