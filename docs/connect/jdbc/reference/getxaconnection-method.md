---
title: getXAConnection 方法 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXADataSource.getXAConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2710613-78b1-438f-b996-c7ae6f34381a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c4e5b96ed5d008e374884597197a735ec72f767
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910148"
---
# <a name="getxaconnection-method-"></a>getXAConnection 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  嘗試建立可用於分散式交易中的實體資料庫連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.sql.XAConnection getXAConnection()  
```  
  
## <a name="return-value"></a>傳回值  
 XAConnection 物件。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 getXAConnection 方法是由 javax.sql.XADataSource 介面中的 getXAConnection 方法所指定。  
  
> [!NOTE]  
>  這個方法通常是由 XA 連接集區實作所呼叫，而不是由一般的 JDBC 應用程式碼所呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [getXAConnection 方法 &#40;SQLServerXADataSource&#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [SQLServerXADataSource 方法](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource 成員](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource 類別](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
