---
title: createBlob 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 630a93b0-6e3c-4255-a007-1097ce0ee243
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3d70c72b860044a7e61b4a6dc5474c465fb60e89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955390"
---
# <a name="createblob-method-sqlserverconnection"></a>createBlob 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  直接建立 Blob 物件，而不使用任何資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Blob createBlob()  
```  
  
## <a name="return-value"></a>傳回值  
 Blob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 createBlob 方法是由連接介面中的 createBlob 方法指定。  
  
 這個方法會取代[SQLServerBlob 函數&#40;SQLServerConnection, byte&#41;](../../../connect/jdbc/reference/sqlserverblob-constructor-sqlserverconnection-byte.md)的需求。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
