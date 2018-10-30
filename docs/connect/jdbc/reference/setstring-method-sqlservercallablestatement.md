---
title: setString 方法 (SQLServerCallableStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f38b97b5-d4f0-4f74-a33d-740241a85842
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b36100c0a2b87abad223c47fc4c81dd802c16cc7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682606"
---
# <a name="setstring-method-sqlservercallablestatement"></a>setString 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 Java **String** 值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setString(java.lang.String sCol,  
                      java.lang.String s)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 **String**，其中包含參數的名稱。  
  
 *s*  
  
 **字串**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setString 方法是由 java.sql.CallableStatement 介面中的 setString 方法指定。  
  
 只有當 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 知道目標類型是二進位時，才可執行字串到二進位的轉換。 在 JDBC 驅動程式不知道基礎類型為何的情況下，它將傳遞 **String** 常值，並在伺服器無法執行轉換作業時傳回伺服器錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
