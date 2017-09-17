---
title: "常見問題集 (FAQ) 適用於 ODBC Linux 和 macOS |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aa835ce2bb9e35191d9c3056dad2f208445c361a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>常見問題集 (FAQ) 適用於 ODBC Linux 和 macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

以下是 ODBC 驅動程式的相關問題的答案[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Linux 及 macOS 上。
  
## <a name="frequently-asked-questions"></a>常見問題集

**Linux 或 macOS 上的現有 ODBC 應用程式使用驅動程式的方式為何？**  
您應該可以編譯和執行您已編譯和執行 Linux 或 macOS 使用其他驅動程式上的 ODBC 應用程式。 
  
**哪些功能[!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]此版本的驅動程式支援？**

ODBC driver on Linux 及 macOS 支援中的所有伺服器功能[!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]但 LocalDB 除外。 如需有關[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支援的功能，請參閱[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)。  
  
**驅動程式是否支援 Kerberos 驗證？**  
是的。 如果您有現有的 Kerberos 環境設定，您應該能夠使用連接到伺服器`Trusted_Connection=Yes`DSN 或連接字串選項。 如需詳細資訊，請參閱[使用整合式驗證](../../../connect/odbc/linux-mac/using-integrated-authentication.md)。  
  
**Unicode 編碼應用程式應使用？**  
UTF-8 用於 SQL_CHAR 資料，UTF-16 則用於 SQL_WCHAR 資料。  

**是否有 ODBC 範例可讓我下載以試驗或評估它的驅動程式執行？**

如需範例，請參閱 [使用 ODBC Driver on Linux 的現有 MSDN C++ ODBC 範例](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 。 這也適用於 macOS ODBC 驅動程式。 

**ODBC driver on Linux 或 macOS 開放原始碼？**

否，Linux 和 macOS 上的 ODBC 驅動程式不是開放原始碼產品。  

## <a name="see-also"></a>另請參閱
[安裝的 Microsoft ODBC Driver for SQL Server on Linux 及 macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

