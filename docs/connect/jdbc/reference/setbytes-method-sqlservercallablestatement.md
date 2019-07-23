---
title: setBytes 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f264f1a6-ee35-4eaf-81d8-ecf99f03b35d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 53a75e8bd85a3601673f51111d87c34eb050a980
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974869"
---
# <a name="setbytes-method-sqlservercallablestatement"></a>setBytes 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定參數設定為指定的 **byte** 值陣列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setBytes(java.lang.String sCol,  
                     byte[] b)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 包含參數名稱的**字串**。  
  
 *b*  
  
 **位元組**值的陣列。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 在舊版的驅動程式中，您可以使用 SQLServerCallableStatement.setBytes 來轉換位元組陣列與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型 **date**、**time**、**datetime2** 或 **datetimeoffset** 之間的值。 現在，搭配這些資料類型使用這個方法將會引發例外狀況，指出不支援轉換。  
  
 此 setBytes 方法由 java.sql.CallableStatement 介面中的 setBytes 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
