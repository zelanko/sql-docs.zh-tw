---
title: getSendTimeAsDatetime 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 018d40464d6461cb4182daf5f93139e322517870
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80929202"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這個方法是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增。  
  
 傳回 **sendTimeAsDatetime** 連線屬性的設定。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>傳回值  
 如果會以  datetime[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 類型將 java.sql.Time 值傳送到伺服器，則為 **true**。 如果會以  time[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 類型將 java.sql.Time 值傳送到伺服器，則為 **false**。  
  
## <a name="remarks"></a>備註  
 如需 [sendTimeAsDatetime](../../../connect/jdbc/setting-the-connection-properties.md) 連線屬性的詳細資訊，請參閱**設定連線屬性**。  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) 可讓您以程式設計方式設定 **sendTimeAsDatetime** 連線屬性。  
  
 如需詳細資訊，請參閱[設定 java.sql.Time 值如何傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
