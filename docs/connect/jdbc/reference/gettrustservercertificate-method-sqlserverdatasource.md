---
description: getTrustServerCertificate 方法 (SQLServerDataSource)
title: getTrustServerCertificate 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3a5de057e6a9363f4e3feeace35f2b5105d3cd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434050"
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>getTrustServerCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 **Boolean** 值，這個值會指出是否啟用 trustServerCertificate 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>傳回值  
 如果啟用 trustServerCertificate，則為 **true**。 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 trustServerCertificate 屬性設定為 **true**，則當使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 時，加密通訊層時會自動信任 TLS 憑證。 換句話說，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將不會驗證 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 憑證。 預設值為 **false**。  
  
 如果 trustServerCertificate 屬性設定為 **false**，則 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將會驗證伺服器 TLS/SSL 憑證。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
