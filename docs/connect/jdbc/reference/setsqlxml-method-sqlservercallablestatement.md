---
title: setSQLXML 方法 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: de095cb3-1111-4154-8996-3c2e529e3000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 82e8d1507760591b4e019d5d785eb0cc6a93c3ac
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924918"
---
# <a name="setsqlxml-method-sqlservercallablestatement"></a>setSQLXML 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 SQLXML 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setSQLXML(java.lang.String parameterName,  
                            java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterName*  
  
 **String**，指出參數名稱。  
  
 *xmlObject*  
  
 SQLXML 物件，其中包含參數值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setSQLXML 方法是由 java.sql.CallableStatement 介面中的 setSQLXML 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
