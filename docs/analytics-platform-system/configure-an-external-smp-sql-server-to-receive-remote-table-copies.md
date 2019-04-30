---
title: 設定 SQL Server 以接收遠端資料表複本-Parallel Data Warehouse |Microsoft Docs
description: 描述如何設定外部 SMP SQL Server 執行個體從平行處理資料倉儲接收遠端資料表複本。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ae6799d468d57dec04046b443c613823c0a8cb8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224689"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>設定外部 SMP SQL Server 以接收遠端資料表複本-平行處理資料倉儲
描述如何設定外部 SQL Server 執行個體從平行處理資料倉儲接收遠端資料表複本。  

本主題說明設定遠端資料表複製的組態步驟的其中一個。 如需所有設定步驟，請參閱[Remote Table copy 複製](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>開始之前  
您可以設定外部的 SQL Server 之前，您必須：  
  
-   具有 SQL Server 2008 Enterprise Edition 或更新版本已準備好安裝或已安裝的 Windows 系統。 Windows 系統必須已經設定中的指示，根據[設定外部 Windows 系統以接收遠端資料表複本使用 InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)。  
  
-   設定 SQL Server 執行個體和 Windows 系統的功能與 Windows 系統管理員帳戶。  
  
-   SQL Server 登入帳戶 （如果尚未安裝 SQL Server） 來建立登入並授與目的地資料庫的權限的能力。  
  
## <a name="HowToSQLServer"></a>設定外部 SMP SQL 伺服器以接收遠端資料表複本  
遠端資料表複製功能會將資料表從 SQL Server PDW 應用裝置複製到執行 Windows 系統的外部 SMP SQL Server 資料庫。 設定外部 Windows 系統以接收遠端資料表複本之後, 的下一個步驟是安裝和設定到 Windows 系統上的 SQL Server。  
  
若要設定 SQL Server，請使用下列步驟：  
  
1.  Windows 系統上安裝 SQL Server 2008 Enterprise Edition 或更新版本。 這被指與 SMP SQL Server。  
  
2.  設定 SQL Server 以接受固定的 TCP 連接埠上的 TCP/IP 連接。 此設定預設為停用，必須啟用才能允許連線到 SMP SQL Server 的 SQL Server PDW。  
  
3.  停用 Windows 防火牆，或設定 SMP SQL Server TCP 連接埠，讓它能夠搭配啟用的 Windows 防火牆。  
  
4.  設定 SQL Server 以允許 SQL Server 驗證模式。 平行處理的資料匯出一律會使用 SQL Server 帳戶進行驗證。  
  
5.  決定將用於驗證 SMP SQL Server 上的 SQL Server 帳戶。 授與該帳戶的建立、 卸除，並將資料插入資料表的平行處理資料匯出作業的目的地資料庫中的權限。  
  
## <a name="BPSQLConfig"></a>遠端資料表複製的 SMP SQL Server 組態的最佳做法  
設定 SMP SQL Server，以接收遠端資料表複本時，使用下列最佳作法，以改善效能。  
  
1.  SQL Server 產品文件中所述，請遵循最佳做法。 例如，啟用資料加密。 如需有關保護 SQL Server 的詳細資訊，請參閱 <<c0> [ 保護 SQL Server 的](../relational-databases/security/securing-sql-server.md)MSDN 上。  
  
2.  使用大量記錄或簡單復原模式。  
  
    在平行處理資料期間匯出作業，資料會大量插入至新建立的目的地資料表。 大量插入期間的最大效能，設定目的地資料庫使用大量記錄或簡單復原模式。  
  
3.  若要回收記錄空間使用 batch_size 選項。  
  
    大量記錄或簡單復原模式使用最低限度記錄大量插入資料，雖然仍會進行一些記錄。 若要避免記錄檔變得太大，使用 SQL Server batch_size 選項以定期回收記錄空間。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
