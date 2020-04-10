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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a7fb65620f619f0bd6f83208be707cd165e4b58
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920545"
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
  
  
