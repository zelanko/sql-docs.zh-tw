---
title: ODBC Linux 和 macOS 的常見問題集 (FAQ) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: aadbf8d0cc850d71626663883587195a8229ada8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66785854"
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>ODBC Linux 和 macOS 的常見問題集 (FAQ)
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

以下是 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Linux 和 macOS 相關問題的解答。
  
## <a name="frequently-asked-questions"></a>常見問題集

**Linux 或 macOS 上的現有 ODBC 應用程式如何使用驅動程式？**  
您應可使用其他驅動程式來編譯及執行您已在 Linux 或 macOS 上編譯和執行的 ODBC 應用程式。 
  
**此版本的驅動程式支援 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 的哪些功能？**

ODBC Driver on Linux 和 macOS 支援 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中的所有伺服器功能，但 LocalDB 除外。 如需詳細資訊[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援的功能，請參閱[Programming Guidelines](../../../connect/odbc/linux-mac/programming-guidelines.md)。  
  
**驅動程式是否支援 Kerberos 驗證？**  
是的。 如果您有現有的 Kerberos 環境設定時，您應該能夠連線到伺服器，使用`Trusted_Connection=Yes`DSN 或連接字串選項。 如需詳細資訊，請參閱[使用整合式驗證](../../../connect/odbc/linux-mac/using-integrated-authentication.md)。  
  
**應用程式應使用哪個 Unicode 編碼？**  
UTF-8 用於 SQL_CHAR 資料，UTF-16 則用於 SQL_WCHAR 資料。  

**是否有 ODBC 範例可讓我下載並與驅動程式一起執行，以試驗或評估驅動程式？**

如需範例，請參閱 [使用 ODBC Driver on Linux 的現有 MSDN C++ ODBC 範例](https://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 。 這也是適用於 macOS 的 ODBC 驅動程式。 

**ODBC 驅動程式位於 Linux 或 macOS 的開放原始碼嗎？**

否，在 Linux 和 macOS 上的 ODBC 驅動程式不是開放原始碼產品。  

## <a name="see-also"></a>另請參閱
[在 Linux 和 macOS 上安裝 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
