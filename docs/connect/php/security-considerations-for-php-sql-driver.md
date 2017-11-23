---
title: "PHP SQL 驅動程式的安全性考量 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: security considerations
ms.assetid: a8c1a570-9204-454f-b94c-ba34f54d487c
caps.latest.revision: "37"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e60c87b9ec5f327460cdbc781ed40cb4a75edb0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="security-considerations-for-php-sql-driver"></a>PHP SQL 驅動程式的安全性考量
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題說明在開發、部署和執行使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的應用程式時特有的安全性考量。 如需關於 SQL Server 安全性的詳細資訊，請參閱 [資料安全性和法規遵循](http://go.microsoft.com/fwlink/?LinkId=129225)。  
  
## <a name="connect-using-windows-authentication"></a>使用 Windows 驗證進行連接  
可能的話，Windows 驗證應該用來連接 SQL Server，原因如下：  
  
-   **在驗證期間不會透過網路傳遞任何認證。** 使用者名稱和密碼不會內嵌在資料庫連接字串中。 這表示惡意使用者或攻擊者無法藉由監視網路或檢視組態檔內的連接字串來取得認證。  
  
-   **使用者受到集中的帳戶管理。** 會強制執行安全性原則，例如；密碼到期日、最小密碼長度，以及帳戶在多次無效登入要求後鎖定。  
  
如需如何使用 Windows 驗證連接到伺服器的相關資訊，請參閱 [如何：使用 Windows 驗證進行連接](../../connect/php/how-to-connect-using-windows-authentication.md)。  
  
當您使用 Windows 驗證進行連接時，建議您設定您的環境，讓 SQL Server 可以使用 Kerberos 驗證通訊協定。 如需詳細資訊，請參閱 [對 SQL Server 2005 的執行個體建立遠端連接時如何確實使用 Kerberos 驗證](http://go.microsoft.com/fwlink/?LinkId=121862) 或 [Kerberos 驗證和 SQL Server](http://go.microsoft.com/fwlink/?LinkId=129226)。  
  
## <a name="use-encrypted-connections-when-transferring-sensitive-data"></a>在傳送敏感性資料時使用加密連接  
在每次要對 SQL Server 傳送或擷取敏感性資料時，均應使用加密連接。 如需如何啟用加密的連接資訊，請參閱[如何啟用加密連接到 Database Engine （SQL Server 組態管理員）](http://go.microsoft.com/fwlink/?LinkId=121864)。 若要使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]建立安全連接，請在連接到伺服器時使用 Encrypt 連接屬性。 如需連接屬性的詳細資訊，請參閱 [Connection Options](../../connect/php/connection-options.md)。  
  
## <a name="use-parameterized-queries"></a>使用參數化查詢  
使用參數化查詢，可降低 SQL 資料隱碼攻擊的風險。 如需執行參數化查詢的範例，請參閱 [How to: Perform Parameterized Queries](../../connect/php/how-to-perform-parameterized-queries.md)。  
  
如需 SQL 資料隱碼攻擊和相關安全性考量的詳細資訊，請參閱 [SQL 資料隱碼](http://go.microsoft.com/fwlink/?LinkId=104224)。  
  
## <a name="do-not-accept-server-or-connection-string-information-from-end-users"></a>不接受來自一般使用者的伺服器或連接字串資訊  
所撰寫的應用程式，應讓使用者無法將伺服器或連接字串資訊提交至應用程式。 對伺服器和連接字串資訊保有嚴格的控制，能夠減少惡意活動的接觸區域。  
  
## <a name="turn-warningsaserrors-on-during-application-development"></a>在應用程式開發期間開啟 WarningsAsErrors  
開發應用程式時應將 **WarningsAsErrors** 設定設為 **true** ，讓驅動程式發出的警告被視為錯誤。 這可讓您在部署應用程式之前及早處理警告。 如需詳細資訊，請參閱 [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md)。  
  
## <a name="secure-logs-for-deployed-application"></a>已部署之應用程式的安全記錄檔  
對於已部署的應用程式，請確實將記錄檔寫入至安全的位置，或是關閉記錄。 這有助於防止一般使用者存取已寫入至記錄檔的資訊。 如需詳細資訊，請參閱 [Logging Activity](../../connect/php/logging-activity.md)。  
  
## <a name="see-also"></a>另請參閱  
[PHP SQL 驅動程式程式設計指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  
