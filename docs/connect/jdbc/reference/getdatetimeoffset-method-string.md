---
title: getDateTimeOffset 方法 (String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fedb1d75-0c3d-4eb3-ae65-da0e153265cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a8aaa3e0d75bdea1817cccf65ce71f88361a1359
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80917788"
---
# <a name="getdatetimeoffset-method-string"></a>getDateTimeOffset 方法 (String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這個方法是在 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增。  
  
 使用 Java 程式設計語言，以指定的參數索引來擷取指定的參數值作為 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 參數的名稱。  
  
## <a name="return-value"></a>傳回值  
 [DateTimeOffset 類別](../../../connect/jdbc/reference/datetimeoffset-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 您可以搭配 [SQLServerCallableStatement.setDateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) 設定 [DateTimeOffset 類別](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)參數值。  
  
## <a name="see-also"></a>另請參閱  
 [getDateTimeOffset 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
