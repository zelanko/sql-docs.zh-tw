---
title: getApplicationName 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f71e501c-ccd7-4a1e-b6ea-4d47a81c18c6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7396b679dce0e655ae6124b1198afc306151ac97
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798973"
---
# <a name="getapplicationname-method-sqlserverdatasource"></a>getApplicationName 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回應用程式名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getApplicationName()  
```  
  
## <a name="return-value"></a>傳回值  
 一個包含應用程式名稱的**字串**，如果未設定任何值，則為 "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]"。  
  
## <a name="remarks"></a>Remarks  
 此應用程式名稱會用來識別各種 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分析工具與記錄工具中的特定應用程式。 如果未設定應用程式名稱，getApplicationName 方法會傳回未當地語系化的字串 "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]"。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
