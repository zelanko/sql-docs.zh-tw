---
title: getString 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getString (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f67371e0-e879-4188-85fc-ecb85f0be2a9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 208fbad8a728775c8e8d985a6f7f28c7facc865f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773488"
---
# <a name="getstring-method-javalangstring"></a>getString 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式語言，並配合指定參數名稱來擷取指定參數的值當作**字串**。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getString(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 **字串**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getString 方法是由 java.sql.CallableStatement 介面中的 getString 方法指定。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的所有資料行都可以當作字串傳回。 這表示可以傳回所有數字和字元類型的字串表示法以及二進位資料行的十六進位字串表示法，例如 binary、varbinary、varbinary(max)、image、timestamp 和 uniqueidentifier。  
  
 區分位置的型別 (例如 money、smallmoney、datetime、smalldatetime、float、real、decimal 和 numeric) 將會針對該型別的基礎值傳回標準 toString() 格式。  
  
 使用者定義型別會當做十六進位字串值傳回。  
  
## <a name="see-also"></a>另請參閱  
 [getString 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
