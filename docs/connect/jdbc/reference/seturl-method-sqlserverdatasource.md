---
title: setURL 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29e1b67caaf566f04cf01c7c93a5e8d2445c31ef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633946"
---
# <a name="seturl-method-sqlserverdatasource"></a>setURL 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用來連接到資料來源的 URL。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>參數  
 *url*  
  
 包含 URL 的**字串**。  
  
## <a name="remarks"></a>Remarks  
 基於安全性理由，您不應該在提供給 setURL 方法的 URL 中包含密碼。 原因是因為協力廠商 Java 應用程式伺服器會經常顯示其資料來源組態使用者介面中所設定的 URL 屬性值。 請改用 [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) 方法來設定密碼值。 這樣一來，Java 應用程式伺服器將不會顯示其資料來源組態使用者介面中所設定的密碼。  
  
> [!NOTE]  
>  如果在呼叫 [getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md) 方法之前未呼叫 setURL 方法，getURL 會傳回預設值 "jdbc:sqlserver://"。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
