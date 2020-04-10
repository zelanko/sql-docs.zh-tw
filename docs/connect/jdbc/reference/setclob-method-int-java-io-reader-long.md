---
title: setClob 方法 (int, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 157882dd-1a96-4501-a895-46e88a49266e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 373af12cda9700eeab6912baf21c12015c1a82d3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927161"
---
# <a name="setclob-method-int-javaioreader-long"></a>setClob 方法 (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定指定的參數為指定的 Reader 物件，該物件長度為指定的字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setClob(int parameterIndex,  
                          java.io.Reader reader,  
                          long length)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterIndex*  
  
 指出參數索引的 **int**。  
  
 *reader*  
  
 Reader 物件。  
  
 *length*  
  
 指出參數值中字元數的 **long**。  
  
## <a name="remarks"></a>備註  
 這個 setClob 方法由 java.sql.PreparedStatement 介面中的 setClob 方法指定。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>另請參閱  
 [setClob 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
