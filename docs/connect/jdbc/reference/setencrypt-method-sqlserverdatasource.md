---
title: setEncrypt 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setEncrypt Method (SQLServerDataSource)
apilocation:
- setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da0aa987f1ec773e2f61e738bc4045136c64859a
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219231"
---
# <a name="setencrypt-method-sqlserverdatasource"></a>setEncrypt 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定 **Boolean** 值，這個值會指出是否啟用 encrypt 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>參數  
 *encrypt*  
  
 如果在用戶端與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之間啟用傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 加密，則為 **true**， 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 encrypt 屬性已設定為 **true**，則 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會確保 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將針對用戶端和伺服器之間傳送的所有資料使用 TLS 加密，條件是伺服器上必須先安裝憑證。 預設值為 **false**。  
  
 JDBC Driver 會在嘗試建立 TLS 交握時偵測其要執行於哪一部 JAVA 虛擬機器 (JVM) 中。  
  
 如果 encrypt 屬性設定為 **true**，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 會使用 JVM 的預設 JSSE 安全性提供者與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 交涉 TLS 加密。 預設的安全性提供者可能不支援成功交涉 TLS 加密所需的所有功能。 例如，預設的安全性提供者可能不支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TLS/SSL 憑證中所使用 RSA 公開金鑰的大小。 在此情況下，預設的安全性提供者可能會引發錯誤，造成 JDBC 驅動程式中止連接。 若要解決這個問題，請執行下列其中之一：  
  
-   使用具有較小 RSA 公開金鑰的伺服器憑證設定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   設定 JVM 在 "\<Java 主目錄>/lib/security/java.security" 安全性屬性檔中使用不同的 JSSE 安全性提供者  
  
-   使用不同的 JVM  
  
 如果 encrypt 屬性未指定或設定為 **false**，則驅動程式將不會強制 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援 TLS 加密。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體未設定為強制 TLS 加密，則不使用任何加密就可以建立連線。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體設定為強制 TLS 加密，則在正確設定的 JAVA 虛擬機器 (JVM) 上執行時，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 將會自動啟用 TLS 加密，否則連線會終止，且驅動程式會引發錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
