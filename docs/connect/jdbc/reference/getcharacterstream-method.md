---
title: getCharacterStream 方法 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70a5a8c8-791a-43f9-8a0e-1c390f30857c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55f50865ce1437ca3611e08836cd6354e4d3d113
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80907414"
---
# <a name="getcharacterstream-method-"></a>getCharacterStream 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 **CLOB** 資料作為 Reader物件或字元資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Reader getCharacterStream()  
```  
  
## <a name="return-value"></a>傳回值  
 Reader 物件，包含 **CLOB** 資料。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getCharacterStream 方法是由 java.sql.Clob 介面中的 getCharacterStream 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
