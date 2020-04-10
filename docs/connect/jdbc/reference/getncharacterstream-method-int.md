---
title: getNCharacterStream 方法 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6ae704f5-823c-4dfe-8c08-07b547c61a3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e5f0aac7395093a38eb50672aa954106713076be
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80905916"
---
# <a name="getncharacterstream-method-int"></a>getNCharacterStream 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的參數索引，擷取所指定參數的值來作為 Reader 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.io.Reader getNCharacterStream(int parameterIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 指出參數索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 Reader 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 存取 **NCHAR**、**NVARCHAR** 和 **LONGNVARCHAR** 參數時，應該使用這個方法。  
  
 這個 getNCharacterStream 方法是由 java.sql.CallableStatement 介面中的 getNCharacterStream 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [getNCharacterStream 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
