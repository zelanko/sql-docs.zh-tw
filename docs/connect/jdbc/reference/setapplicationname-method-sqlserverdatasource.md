---
description: setApplicationName 方法 (SQLServerDataSource)
title: setApplicationName 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 24d6e48d-53c4-4da2-a6de-1cdff463c9cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e237100c0c1da4ad9188da943412891d808a735c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432660"
---
# <a name="setapplicationname-method-sqlserverdatasource"></a>setApplicationName 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定應用程式名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setApplicationName(java.lang.String applicationName)  
```  
  
#### <a name="parameters"></a>參數  
 *applicationName*  
  
 包含應用程式名稱的 **String**。  
  
## <a name="remarks"></a>備註  
 此應用程式名稱會用來識別各種 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分析工具與記錄工具中的特定應用程式。 如果未設定應用程式名稱，getApplicationName 方法會傳回未當地語系化的字串 "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]"。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
