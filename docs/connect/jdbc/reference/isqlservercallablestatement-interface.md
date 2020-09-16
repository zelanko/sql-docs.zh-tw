---
description: ISQLServerCallableStatement 介面
title: ISQLServerCallableStatement 介面 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 030a1631-cfcd-41e0-beb5-47f93c01e8e0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf06f6489ab4df31a2032d6e7044f88ac1538fc6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433540"
---
# <a name="isqlservercallablestatement-interface"></a>ISQLServerCallableStatement 介面
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表 JDBC 可呼叫陳述式。 這個介面是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.sql.CallableStatement、[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
public interface ISQLServerCallableStatement  
```  
  
## <a name="remarks"></a>備註  
 此介面是由 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)所實作。  
  
 此介面會公開下列 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 的特定方法：  
  
|方法|如需相關資訊，請參閱|  
|------------|-------------------------------|  
|microsoft.sql.DateTimeOffset getDateTimeOffset(int)|[getDateTimeOffset(int)](../../../connect/jdbc/reference/getdatetimeoffset-method-int.md)|  
|microsoft.sql.DateTimeOffset getDateTimeOffset(String)|[getDateTimeOffset(String)](../../../connect/jdbc/reference/getdatetimeoffset-method-string.md)|  
|void setDateTimeOffset(String, microsoft.sql.DateTimeOffset)|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
