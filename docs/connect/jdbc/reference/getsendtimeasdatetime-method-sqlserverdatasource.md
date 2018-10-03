---
title: getSendTimeAsDatetime 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f18836d12be9834512783f90a2d7730fcfc98798
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845206"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這個方法是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增。  
  
 傳回的設定**sendTimeAsDatetime**連接屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>傳回值  
 **true** java.sql.Time 值如果會傳送至伺服器，當做[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime**型別。 **false** java.sql.Time 值如果會傳送至伺服器，當做[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**時間**型別。  
  
## <a name="remarks"></a>Remarks  
 請參閱[設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)如需詳細資訊**sendTimeAsDatetime**連接屬性。  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 可讓您以程式設計方式設定 **sendTimeAsDatetime** 連線屬性。  
  
 如需詳細資訊，請參閱 <<c0> [ 如何設定 java.sql.Time 值傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
