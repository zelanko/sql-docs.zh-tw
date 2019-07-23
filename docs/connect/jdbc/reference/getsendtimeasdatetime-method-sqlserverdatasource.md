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
ms.openlocfilehash: e1396ac28a7e41dbf530f7e4a251876f6c340871
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979940"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這個方法是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增。  
  
 傳回**sendTimeAsDatetime**連接屬性的設定。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>傳回值  
 如果將 java. Time 值當做**datetime**類型傳送到伺服器[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ,**則為 true** 。 如果將 java. time 值當做**時間**類型傳送到伺服器[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , 則為**false** 。  
  
## <a name="remarks"></a>Remarks  
 如需**sendTimeAsDatetime**連接屬性的詳細資訊, 請參閱[設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)。  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 可讓您以程式設計方式設定 **sendTimeAsDatetime** 連線屬性。  
  
 如需詳細資訊, 請參閱設定將[java. Time 值傳送至伺服器的方式](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
