---
title: setLoginTimeout 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83d6869075e296465ee9c60b0c5032407d4fe2da
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925758"
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>setLoginTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定這個 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件在嘗試建立連接時將等候的秒數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>參數  
 *loginTimeout*  
  
 **int** 值，代表要等候的秒數。 零值代表此逾時為預設系統逾時，預設指定為 15 秒。  
  
## <a name="remarks"></a>備註  
 這個 setLoginTimeout 方法是由 javax.sql.DataSource 介面中的 setLoginTimeout 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
