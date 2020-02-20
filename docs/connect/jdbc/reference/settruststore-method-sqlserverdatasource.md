---
title: setTrustStore 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustStore Method (SQLServerDataSource)
apilocation:
- setTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: bab5485d-4547-426c-adbe-44e2b5702d1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be54aea70e712d2209c04196d3e450bca488578b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972189"
---
# <a name="settruststore-method-sqlserverdatasource"></a>setTrustStore 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定憑證 trustStore 檔案的路徑 (包括檔案名稱)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTrustStore(java.lang.String trustStore)  
```  
  
#### <a name="parameters"></a>參數  
 *trustStore*  
  
 **String**，其中包含憑證 trustStore 檔案的路徑 (包括檔案名稱)。  
  
## <a name="remarks"></a>備註  
 如果未指定 trustStore 屬性或將其設定為 null，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將會依賴信任管理員 Factory 的查閱規則，決定要使用的憑證存放區。 預設的 SunX509 TrustManagerFactory 會嘗試以下列搜尋位置順序，找出信任的資料：  
  
-   1. 由 "javax.net.ssl.trustStore" Java Virtual Machine (JVM) 系統屬性所指定的檔案。  
  
-   2. "\<java-home>/lib/security/jssecacerts" 檔案。  
  
-   3. "\<java-home>/lib/security/cacerts" 檔案。  
  
 如需詳細資訊，請參閱 Sun Microsystems 網站上的 SunX509 TrustManager 介面文件。  
  
 如果 trustStore 屬性設定為字串或是空字串 ""，驅動程式將會使用該值來找出 trustStore 檔案，以便驗證伺服器 SSL 憑證。  
  
 trustStorePassword 屬性可以隨著 trustStore 屬性一起指定，而其值可用來開啟 trustStore 檔案。 如需詳細資訊，請參閱 [setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
