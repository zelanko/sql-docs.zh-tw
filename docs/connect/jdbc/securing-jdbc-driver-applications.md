---
title: "保護 JDBC 驅動程式應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8033e1690fcaa01ca73ce1a7d0d9972ac2d3ba9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="securing-jdbc-driver-applications"></a>保護 JDBC Driver 應用程式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  增強的安全性[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]應用程式牽涉到避免常犯的編碼錯誤而已。 存取資料的應用程式有許多攻擊者可以用於擷取、操作或破壞敏感性資料的潛在錯誤點。 了解安全性的各個層面相當重要，包括在應用程式的設計階段處理威脅模型到其最終的部署，以及繼續持續的維護。  
  
 本節中的主題描述一些常見的安全性考量，包括連接字串、驗證使用者輸入，以及一般應用程式安全性。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[保護連接字串](../../connect/jdbc/securing-connection-strings.md)|描述協助保護連接資料來源時所使用之資訊的技術。|  
|[驗證使用者輸入](../../connect/jdbc/validating-user-input.md)|描述驗證使用者輸入的技術。|  
|[應用程式安全性](../../connect/jdbc/application-security.md)|描述如何使用 Java 原則權限協助保護 JDBC 驅動程式應用程式。|  
|[使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)|描述如何建立使用安全通訊通道[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫使用安全通訊端層 (SSL)。|  
|[在 FIPS 模式](../../connect/jdbc/fips-mode.md)|描述如何在 FIPS complainant 模式中使用 JDBC 驅動程式。| 
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
