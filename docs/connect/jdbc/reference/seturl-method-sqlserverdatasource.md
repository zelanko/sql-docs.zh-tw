---
title: setURL 方法 (SQLServerDataSource) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e13927cc02d9b995ac3c99a5b0a4b490328b8dbf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="seturl-method-sqlserverdatasource"></a>setURL 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用來連接到資料來源的 URL。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>參數  
 *Url*  
  
 A**字串**包含 URL。  
  
## <a name="remarks"></a>備註  
 基於安全性理由，您不應該將密碼包含在提供給 setURL 方法的 URL。 原因是因為協力廠商 Java 應用程式伺服器會經常顯示其資料來源組態使用者介面中所設定的 URL 屬性值。 請改用[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)方法來設定密碼值。 這樣一來，Java 應用程式伺服器將不會顯示其資料來源組態使用者介面中所設定的密碼。  
  
> [!NOTE]  
>  如果未呼叫 setURL 方法呼叫之前[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)方法，getURL 會傳回預設值"sqlserver: / /"。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
