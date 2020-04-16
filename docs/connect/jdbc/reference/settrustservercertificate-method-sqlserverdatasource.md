---
title: setTrustServerCertificate 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea37bbfb1582836db8f0c12b383b59c2d527f5ef
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219188"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>setTrustServerCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定 **Boolean** 值，這個值會指出是否啟用 trustServerCertificate 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>參數  
 *trustServerCertificate*  
  
 如果在使用傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 加密通訊層時需自動信任 TLS 憑證，則為 **true**， 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 trustServerCertificate 屬性設定為 **true**，則當使用 TLS 加密通訊層時會自動信任 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 憑證。 換句話說，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將不會驗證 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 憑證。 預設值為 **false**。  
  
 如果 trustServerCertificate 屬性設定為 **false**，則 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將會驗證伺服器 TLS/SSL 憑證。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
