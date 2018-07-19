---
title: Microsoft ODBC Driver for SQL Server on Windows 的功能 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e2b7c107a40a60a1da5ed891d7a26a7c85011db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32856333"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server on Windows 的功能
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQL Server on Windows

適用於 SQL Server ODBC Driver 13.1 包含舊版 (11) 的所有功能，並且加入了 永遠加密和 Azure Active Directory 驗證時用於搭配 Microsoft SQL Server 2016 支援。  
  
一律加密可讓用戶端將用戶端應用程式內的機密資料進行加密，且永遠不會顯示 SQL Server 的加密金鑰。 安裝在用戶端電腦上且啟用一律加密的驅動程式，透過自動將 SQL Server 用戶端應用程式中的機密資料進行加密與解密，進而達成此目的。 驅動程式會先將敏感資料行中的資料進行加密，才會將資料傳遞至 SQL Server，並自動重寫查詢以保留應用程式的語意。 同樣地，驅動程式會以透明的方式，將查詢結果中加密資料庫資料行所儲存的資料進行解密。 如需詳細資訊，請參閱[的 ODBC 驅動程式搭配使用一律加密](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)。
 
Azure Active Directory 可讓使用者、 DBA 和應用程式設計人員使用 Azure Active Directory 驗證做為機制的 Azure Active Directory (Azure AD 中使用身分識別連接到 Microsoft Azure SQL Database 和 Microsoft SQL Server 2016). 如需詳細資訊，請參閱[使用 Azure Active Directory 與 ODBC 驅動程式](../../../connect/odbc/using-azure-active-directory.md)，和[連接到 SQL Database 或 SQL 資料倉儲使用 Azure Active Directory 驗證](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/)。   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver 11 for SQL Server  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 包含隨附於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 的 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]Native Client ODBC 驅動程式的所有功能。 如需詳細資訊，請參閱 [SQL Server Native Client 程式設計](http://msdn.microsoft.com/library/ms130892.aspx)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ODBC 驅動程式以 Windows 作業系統中隨附的 ODBC 驅動程式作為基礎。 如需詳細資訊，請參閱 [Windows Data Access Components SDK](http://msdn.microsoft.com/library/aa968814(VS.85).aspx)。  
  
此版本的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 包含下列新功能：  
  
### <a name="bcpexe-l-option-for-specifying-a-login-timeout"></a>bcp.exe – l 選項指定登入逾時
 
– L 選項會指定之前的秒數`bcp.exe`登入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]逾時當您嘗試連接到伺服器。 預設登入逾時是 15 秒。 登入逾時必須是介於 0 到 65534 之間的數字。 如果所提供的值不是數值或不在該範圍內，`bcp.exe` 就會產生錯誤訊息。 值為 0 會指定無限逾時。 小於 10 秒 （大約） 的登入逾時並不可靠。  
  
### <a name="driver-aware-connection-pooling"></a>可感知驅動程式的連接共用  
ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支援[感知驅動程式的連接共用](http://msdn.microsoft.com/library/hh405031(VS.85).aspx)。 如需詳細資訊，請參閱 [Driver-Aware Connection Pooling in the ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。  
  
### <a name="asynchronous-execution-notification-method"></a>非同步執行 (通知方法)  
ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支援[非同步執行 （通知方法）](http://msdn.microsoft.com/library/hh405038(VS.85).aspx)。 如需使用範例，請參閱[非同步執行&#40;通知方法&#41;範例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)。  
  
### <a name="connection-resiliency"></a>連接恢復功能
若要確保應用程式仍然連接到 Microsoft Azure SQL Database，Windows 上的 ODBC 驅動程式可以還原閒置的連接。 如需詳細資訊，請參閱 [Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)。  
  
## <a name="behavior-changes"></a>行為變更

在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Native Client，`-y0`選項`sqlcmd.exe`造成的顯示寬度是 0，如果在 1 MB 處截斷輸出。
  
從 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，可在單一資料行中擷取的資料量沒有限制時`–y0`指定。 `sqlcmd.exe` 現在，串流處理達 2 GB 的資料行 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料類型最大值)。  
  
另一項差異是指定這兩者`-h`和`-y0`現在會產生錯誤報告選項不相容。 `-h`指定資料行標頭之間列印的資料列數目以及從未相容`-y0`，已略過，雖然不列印任何標頭。
  
請注意，`-y0`會造成效能問題的伺服器和網路，視傳回的資料大小而定。

## <a name="see-also"></a>另請參閱  
[Windows 上適用於 SQL Server 的 Microsoft ODBC 驅動程式](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
