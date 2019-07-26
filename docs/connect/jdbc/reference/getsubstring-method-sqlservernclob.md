---
title: getSubString 方法 (SQLServerNClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1d91c930-1bac-4da9-b9a5-ac2cfd31541b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf2caa03e047bb53ca946153205492c417448e85
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979324"
---
# <a name="getsubstring-method-sqlservernclob"></a>getSubString 方法 (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  依據所指定開始位置和要複製的字元數，擷取 **NCLOB** 中所指定子字串的複本。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getSubString(long pos,  
                                  int length)  
```  
  
#### <a name="parameters"></a>參數  
 *pos*  
  
 要從子字串中擷取的第一個字元。 第一個字元落在位置 1。  
  
 *length*  
  
 要複製的連續字元數目。  
  
## <a name="return-value"></a>傳回值  
 **String**，它是 **NCLOB** 中指定的子字串。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getSubString 方法是由 java.sql.NClob 介面中的 getSubString 方法指定。  
  
 嘗試從 null 或零長度 NCLOB 中取得零個字元，將會傳回空字串。 嘗試在零長度 NCLOB 中的位置 1 以外之任何位置取得任何長度的字元，將會擲回位置例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
