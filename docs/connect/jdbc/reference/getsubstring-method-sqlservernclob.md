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
manager: craigg
ms.openlocfilehash: f283115f4629e778d9b6fc4a94ccaf85064da6c4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648956"
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
 A**字串**也就是指定的子字串中**NCLOB**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 GetSubString 方法 java.sql.NClob 介面中所指定這個 getSubString 方法。  
  
 嘗試從 null 或零長度 NCLOB 中取得零個字元，將會傳回空字串。 嘗試在零長度 NCLOB 中的位置 1 以外之任何位置取得任何長度的字元，將會擲回位置例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成員](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 類別](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
