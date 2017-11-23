---
title: "setEncrypt 方法 (SQLServerDataSource) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: setEncrypt Method (SQLServerDataSource)
apilocation: setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e90e49bff2956be8aa6950ec9612ea534921aac
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="setencrypt-method-sqlserverdatasource"></a>setEncrypt 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定**布林**值，指出是否啟用 encrypt 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>參數  
 *加密*  
  
 **true**如果用戶端之間啟用安全通訊端層 (SSL) 加密和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 encrypt 屬性設定為**true**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]可確保[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]如果伺服器已安裝憑證，用戶端與伺服器之間傳送的所有資料使用 SSL 加密。 預設值是 **false**秒。  
  
 JDBC Driver 會在嘗試建立 SSL 交握時偵測其要執行於哪一個 Java Virtual Machine (JVM) 中。  
  
 如果 encrypt 屬性設定為**true**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]使用 JVM 的預設 JSSE 安全性提供者與交涉 SSL 加密[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。 預設的安全性提供者可能不支援成功交涉 SSL 加密所需的所有功能。 例如，預設安全性提供者可能不支援的大小之 RSA 公開金鑰用於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]SSL 憑證。 在此情況下，預設的安全性提供者可能會引發錯誤，造成 JDBC 驅動程式中止連接。 若要解決這個問題，請執行下列其中之一：  
  
-   設定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]的較小的 RSA 公開金鑰的伺服器憑證  
  
-   設定要使用不同的 JSSE 安全性提供者，在 JVM"\<java 首頁 > / lib/security/java.security"安全性屬性檔  
  
-   使用不同的 JVM  
  
 如果 encrypt 屬性未指定或設為**false**，驅動程式不會強制執行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支援 SSL 加密。 如果[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]執行個體未設定為強制 SSL 加密，不用任何加密建立連線。 如果[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]執行個體設定為強制 SSL 加密，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]會自動啟用 SSL 加密時正確設定上執行 JVM，否則連接會中止，且驅動程式會引發錯誤。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
