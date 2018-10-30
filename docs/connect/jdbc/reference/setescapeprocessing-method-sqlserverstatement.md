---
title: setEscapeProcessing 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setEscapeProcessing
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ac0682e-e04c-4fdb-893b-92408d42051e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52a7931ffe5ffb80f0ca376318e8b50a8e21e6d5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745596"
---
# <a name="setescapeprocessing-method-sqlserverstatement"></a>setEscapeProcessing 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定逸出處理模式。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 的逸出處理一律保持啟用狀態。 設定這個方法成 false 時不會有任何作用。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setEscapeProcessing(boolean enable)  
```  
  
#### <a name="parameters"></a>參數  
 *enable*  
  
 如果啟用逸出處理，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 setEscapeProcessing 方法是由 java.sql.Statement 介面中的 setEscapeProcessing 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
