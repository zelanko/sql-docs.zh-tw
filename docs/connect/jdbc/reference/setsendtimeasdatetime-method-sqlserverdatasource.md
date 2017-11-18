---
title: "setSendTimeAsDatetime 方法 (SQLServerDataSource) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f6a576e4cb3ef155092a1244bbf9e7c2fcaaadd5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>setSendTimeAsDatetime 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這個方法加入在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC 驅動程式 3.0。  
  
 修改的設定**sendTimeAsDatetime**連接屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>參數  
 *sendTimeAsDateTime*  
  
 布林值。 當 true 時，會導致 java.sql.Time 值傳送至伺服器的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime**型別。 若為 false，會導致 java.sql.Time 值傳送至伺服器的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]**時間**型別。  
  
## <a name="remarks"></a>備註  
 [SQLServerDataSource.getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)傳回設定**sendTimeAsDatetime**連接屬性。  
  
 如需有關**sendTimeAsDatetime**連接屬性，請參閱[設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
 如需詳細資訊，請參閱[如何設定 java.sql.Time 值傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

