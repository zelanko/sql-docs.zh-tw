---
title: setNClob 方法 (java.lang.String, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c1b95ee7-7e82-418f-8f30-948589086f63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5d94c56b057c5909ec4d092ad8814258c5eab3e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923301"
---
# <a name="setnclob-method-javalangstring-javaioreader-long"></a>setNClob 方法 (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為所指定 Reader 物件，該物件長度為指定的字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.io.Reader reader,  
              long length)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterName*  
  
 包含參數名稱的**字串**。  
  
 *reader*  
  
 Reader 物件。  
  
 *length*  
  
 **long**，指出資料流中的字元數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此方法應該用於 **NCHAR**、**NVARCHAR**、**NTEXT** 和 **XML** 參數資料類型。  
  
 這個 setNClob 方法是由 java.sql.CallableStatement 介面中的 setNClob 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [setNClob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
