---
title: ISQLServerConnection 介面 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 031c01e2-2c65-4fe4-9700-fdbcc7a39f30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d2f63e094fa4ea4598163d419e221ad5a41b288
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920691"
---
# <a name="isqlserverconnection-interface"></a>ISQLServerConnection 介面
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表與 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的 JDBC 連線。 這個介面是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** java.sql.Connection  
  
## <a name="syntax"></a>語法  
  
```  
  
public interface ISQLServerConnection  
```  
  
## <a name="remarks"></a>備註  
 此介面是由 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)所實作。  
  
 此介面會公開下列 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特有的欄位：  
  
|欄位|如需相關資訊，請參閱|  
|-----------|-------------------------------|  
|public final static int TRANSACTION_SNAPSHOT|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|  
|public UUID getClientConnectionId()|[getClientConnectionID()](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
