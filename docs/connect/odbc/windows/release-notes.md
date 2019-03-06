---
title: 版本資訊 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: cc1321ac161923499d57ab69374b8ed603d272e0
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955769"
---
# <a name="release-notes"></a>版本資訊
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Microsoft ODBC Driver for SQL Server on Windows 版本資訊  


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能

**新增功能**:

- Azure Active Directory 受控服務識別 (系統和使用者指派) 驗證模式，如需詳細資訊，請參閱[使用 Azure Active Directory 與 ODBC 驅動程式](../using-azure-active-directory.md)
- 能夠串流輸入的參數，針對 永遠加密的資料行，如需詳細資訊，請參閱[的 ODBC 驅動程式使用永遠加密時的限制](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)
- XA 分散式交易，如需詳細資訊，請參閱[使用 XA 交易](../use-xa-with-dtc.md)

[ug 修正](../bug-fixes.md)

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能

**新增功能**:

資料分類，Azure SQL Database 和 SQL Server，如需詳細資訊請參閱[資料分類](../data-classification.md)

Utf-8 伺服器版本編碼方式的支援

[ug 修正](../bug-fixes.md)

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能

**新增功能**:

支援`SQL_COPT_SS_CEKCACHETTL`並`SQL_COPT_SS_TRUSTEDCMKPATHS`連接屬性 (如需詳細資訊，請參閱[搭配 ODBC Driver for SQL Server 使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` 可讓控制本機快取的資料行加密金鑰存在的時間，以及排清它
- `SQL_COPT_SS_TRUSTEDCMKPATHS` 允許應用程式限制為只使用指定的清單的資料行主要金鑰的 AE 作業


Azure Active Directory 互動式驗證支援

[ug 修正](../bug-fixes.md)


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能

**新增功能**:

Always Encrypted 支援適用於 BCP API

新的連接字串屬性 UseFMTOnly 會導致驅動程式需要暫存資料表的特殊案例中使用舊版的中繼資料。

Azure SQL 受控執行個體 （延伸私人預覽） 支援。 
> [!NOTE]
> 使用受控執行個體時，有一些差異：
> -   不支援檔案資料流 
> -   本機檔案系統存取不受支援，但所需的 tracefiles 等項目 
> -   建立 UDT，從本機路徑不支援 
> -   不支援 Windows 整合式驗證 
> -   不支援 DTC 
> -   'sa' 帳戶不存在 （預設帳戶稱為 'cloudSA'）
> -   TDS token 錯誤 (0xAA) 傳回不正確的伺服器名稱
> -   不支援資料庫名稱 中的特殊字元 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] 不支援
> -   錯誤訊息一律會顯示在英文中，不論語言為何 （與 Azure 相同） 的設定 
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能  
 ODBC Driver 13.1 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]加入對[Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)並[Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)時用於搭配 Microsoft SQL Server 2016。  對應的連接共用的關鍵字/屬性所述[驅動程式知道連線集區中的 ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能  
 ODBC Driver 13 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]包含先前的功能，從 ODBC Driver 11 for SQL Server，並新增適用於 Microsoft SQL Server 2016 的支援。

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 上 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的新功能  
 ODBC Driver 11 for SQL Server 包含新[功能](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)，以及 SQL Server 2012 Native Client 中隨附於 ODBC 的所有功能。  
