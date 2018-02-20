---
title: "版本資訊 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: 44c73c4d632fd434fcd296dc6fc2cc70af26086c
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2018
---
# <a name="release-notes"></a>版本資訊
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Microsoft ODBC Driver for SQL Server on Windows 版本資訊  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>新功能的[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for 17 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上

**加入功能**:

永遠加密的 BCP API 的支援

新的連接字串屬性 UseFMTOnly 會導致驅動程式需要暫存資料表的特殊案例中使用傳統的中繼資料。

SQL Azure 受管理的執行個體 （擴充私人預覽中） 的支援。 
> [!NOTE]
> 使用受管理的執行個體時，有一些差異：
> -   不支援 FILESTREAM 
> -   不支援，但所需 tracefiles 之類的本機檔案系統存取 
> -   建立 UDT，從本機路徑不支援 
> -   不支援 Windows 整合式驗證 
> -   不支援 DTC 
> -   帳戶 'sa' 不存在 （預設的帳戶稱為 'cloudSA'）
> -   TDS token 的錯誤 (0xAA) 傳回不正確的伺服器名稱
> -   不支援在 資料庫名稱的特殊字元 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] 不支援
> -   錯誤訊息都會顯示在英文中，不論語言為何設定 （如同 Azure） 
  
## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>新功能的[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上  
 ODBC Driver 13.1 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]新增支援[永遠加密](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)和[Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md)時用於搭配 Microsoft SQL Server 2016。  共用的關鍵字/屬性中所述的對應連接[驅動程式知道連線集區中的 ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>新功能的[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上  
 ODBC Driver 13 for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]包含先前的功能，從 ODBC Driver 11 for SQL Server，並且加入了 Microsoft SQL Server 2016 支援。

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>新功能的[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows 上  
 ODBC Driver 11 for SQL Server 包含新[功能](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)以及 SQL Server 2012 Native Client 中 ODBC 隨附的所有功能。  
