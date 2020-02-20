---
title: getBinaryStream (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBinaryStream(int paramIndex)
apilocation:
- SQLServerCallableStatement.getBinaryStream(int paramIndex)
apitype: Assembly
ms.assetid: a766818e-cd05-4a07-a1ae-88966017448c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e5e2a85e2db6dd89e571185712514a27621e835
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953752"
---
# <a name="getbinarystream-int"></a>getBinaryStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在給定參數索引時，擷取指定之參數的值來當做不中斷位元組的二進位資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.io.InputStream getBinaryStream(int paramIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *paramIndex*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>另請參閱  
 [getBinaryStream 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
