---
title: connect 方法 (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.connect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43813a4c-1cc7-4659-ba27-f1786f1371eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a182f62796d70fe50f646f39d1afb7058d46fd8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927728"
---
# <a name="connect-method-sqlserverdriver"></a>connect 方法 (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立與資料庫的連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Connection connect(java.lang.String Url,  
                                   java.util.Properties suppliedProperties)  
```  
  
#### <a name="parameters"></a>參數  
 *Url*  
  
 **String** 值，其中包含用來連接到資料庫的 URL。  
  
 *suppliedProperties*  
  
 當做連接引數使用的一組字串值。  
  
## <a name="return-value"></a>傳回值  
 連線物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 connect 方法是由 java.sql.Driver 介面中的 connect 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成員](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 類別](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
