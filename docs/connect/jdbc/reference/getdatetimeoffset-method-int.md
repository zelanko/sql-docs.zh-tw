---
description: getDateTimeOffset 方法 (int)
title: getDateTimeOffset 方法 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8bb00356-4d6e-4625-b924-67646930fdf2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f4c6aa2bfc8fb8a1045566d79853cdb28a2207a6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436310"
---
# <a name="getdatetimeoffset-method-int"></a>getDateTimeOffset 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這個方法是在 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 驅動程式 3.0 中新增。  
  
 使用 Java 程式設計語言，以指定的參數索引來擷取指定的參數值作為 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(int index)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 以一為基底的參數序數。  
  
## <a name="return-value"></a>傳回值  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 您可以使用 [SQLServerCallableStatement.setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md) 來設定 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)參數值。  
  
## <a name="see-also"></a>另請參閱  
 [getDateTimeOffset 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
