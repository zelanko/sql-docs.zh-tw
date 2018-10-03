---
title: setHostNameInCertificate 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 012073c9d1f8f3646c9bea5fd35cb12e0e0343c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601778"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>setHostNameInCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定用於驗證 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全通訊端層 (SSL) 憑證的主機名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>參數  
 *hostNameInCertificate*  
  
 包含主機名稱的**字串**。  
  
## <a name="remarks"></a>Remarks  
 此 hostNameInCertificate 值會在使用 SSL 加密通訊層時用來驗證 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 憑證。 預設值為 null。  
  
 如果 hostNameInCertificate 屬性設定為 null 或未指定，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將會使用 serverName 屬性值來驗證 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SSL 憑證。 如果 hostNameInCertificate 屬性設定為字串或是空字串 ""，驅動程式將會使用該值來驗證伺服器 SSL 憑證。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
