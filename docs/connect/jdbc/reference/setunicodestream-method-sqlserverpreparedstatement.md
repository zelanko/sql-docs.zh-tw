---
title: setUnicodeStream 方法 (SQLServerPreparedStatement) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a413e83-e0a4-41f8-9fe0-33ce4d368ee4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7478baa859b65ce7c801ae8e9872d51f2e3fec3d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32846443"
---
# <a name="setunicodestream-method-sqlserverpreparedstatement"></a>setUnicodeStream 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定指定的參數數值為給定的輸入資料流，其中將包含指定的位元組數目。  
  
> [!NOTE]  
>  JDBC 規格中已經取代這個方法，呼叫此方法將會擲回「未實作」例外狀況。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setUnicodeStream(int n,  
                                   java.io.InputStream x,  
                                   int length)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 **Int** ，指出參數編號。  
  
 *x*  
  
 InputStream 物件。  
  
 *長度*  
  
 位元組數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setUnicodeStream 方法是由 java.sql.PreparedStatement 介面中的 setUnicodeStream 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
