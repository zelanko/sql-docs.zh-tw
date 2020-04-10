---
title: rollback 方法 (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.rollback
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 93d9d7e6-54b6-4d86-8f8c-386c6057e85e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d129913a4946d5887a100bd4a295c344a951c2f0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80903775"
---
# <a name="rollback-method-sqlserverxaresource"></a>rollback 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  要求資源管理員回復之前代表交易分支所完成的工作。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void rollback(javax.transaction.xa.Xid xid)  
```  
  
#### <a name="parameters"></a>參數  
 *xid*  
  
 Xid 物件。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>備註  
 這個 rollback 方法是由 javax.transaction.xa.XAResource 介面中的 rollback 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
