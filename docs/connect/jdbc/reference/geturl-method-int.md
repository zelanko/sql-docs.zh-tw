---
title: getURL 方法 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getURL Ijnt)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 75d03ced-3614-4997-9abd-24642b1d1aae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe82c5de9932eb7279e07c5eed3b1644c6c57462
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910704"
---
# <a name="geturl-method-int"></a>getURL 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，並配合指定的參數索引來擷取所指定參數值作為 URL 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.net.URL getURL(int n)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 URL 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getURL 方法是由 java.sql.CallableStatement 介面中的 getURL 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getURL 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
