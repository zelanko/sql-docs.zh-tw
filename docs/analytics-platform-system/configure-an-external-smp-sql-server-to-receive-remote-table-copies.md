---
title: 設定 SQL Server 以接收遠端資料表複本
description: 描述如何設定外部 SMP SQL Server 實例，以從平行處理資料倉儲接收遠端資料表複本。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3e5475e86582ede2e6fa7ca5a302bba7ee74faa3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401319"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>設定外部 SMP SQL Server 以接收遠端資料表複本-平行處理資料倉儲
描述如何設定外部 SQL Server 實例，以從平行處理資料倉儲接收遠端資料表複本。  

本主題說明設定遠端資料表複本的其中一個設定步驟。 如需所有設定步驟的清單，請參閱[遠端資料表複本](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>開始之前  
在您可以設定外部 SQL Server 之前，您必須：  
  
-   擁有已準備好安裝或已安裝 SQL Server 2008 Enterprise Edition 或更新版本的 Windows 系統。 Windows 系統必須已根據[設定外部 Windows 系統中的指示，設定為使用「不允許」來接收遠端資料表複本](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)。  
  
-   可以設定 SQL Server 實例和 Windows 系統的 Windows 管理員帳戶。  
  
-   SQL Server 登入帳戶（如果已安裝 SQL Server），而且能夠在目的地資料庫上建立登入和授與許可權。  
  
## <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a><a name="HowToSQLServer"></a>設定外部 SMP SQL Server 以接收遠端資料表複本  
遠端資料表複製功能會將資料表從 SQL Server PDW 設備複製到在 Windows 系統上執行的外部 SMP SQL Server 資料庫。 設定外部 Windows 系統以接收遠端資料表複本之後，下一步就是在 Windows 系統上安裝和設定 SQL Server。  
  
若要設定 SQL Server，請使用下列步驟：  
  
1.  在 Windows 系統上安裝 SQL Server 2008 Enterprise Edition 或更新版本。 這稱為 SMP SQL Server。  
  
2.  設定 SQL Server 以接受固定 TCP 通訊埠上的 TCP/IP 連接。 此設定預設為停用，而且必須啟用以允許 SQL Server PDW 連接到 SMP SQL Server。  
  
3.  請停用 Windows 防火牆或設定 SMP SQL Server TCP 埠，使其可在啟用 Windows 防火牆的情況下使用。  
  
4.  設定 SQL Server 以允許 SQL Server 驗證模式。 平行資料匯出一律會使用 SQL Server 帳戶進行驗證。  
  
5.  判斷將用於驗證之 SMP SQL Server 上的 SQL Server 帳戶。 授與該帳戶建立、卸載及插入資料到目的地資料庫中之資料表的許可權，以進行平行資料匯出工作。  
  
## <a name="best-practices-for-smp-sql-server-configuration-for-remote-table-copy"></a><a name="BPSQLConfig"></a>SMP SQL Server 遠端資料表複本設定的最佳做法  
設定 SMP SQL Server 以接收遠端資料表複本時，請使用下列最佳作法來改善效能。  
  
1.  遵循 SQL Server 產品檔中所述的最佳作法。 例如，啟用資料加密。 如需保護 SQL Server 的詳細資訊，請參閱 MSDN 上的[保護 SQL Server](../relational-databases/security/securing-sql-server.md) 。  
  
2.  使用大容量日誌或簡單復原模式。  
  
    在平行處理資料匯出工作期間，資料會大量插入至新建立的目的地資料表。 如需大量插入期間的最大效能，請將目的地資料庫設定為使用大量記錄或簡單復原模式。  
  
3.  使用 [batch_size] 選項來回收記錄檔空間。  
  
    雖然大量記錄或簡單復原模式對大量插入的資料使用最低限度記錄，但仍會進行一些記錄。 若要防止記錄檔變得太大，請使用 SQL Server batch_size 選項來定期回收記錄檔空間。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
