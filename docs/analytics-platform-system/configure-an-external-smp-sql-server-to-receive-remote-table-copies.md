---
title: "外部 SMP SQL Server 設定為接收遠端資料表的副本 (PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bbd2ed6-064e-4b45-b67b-608dc0f2b2bc
caps.latest.revision: "13"
ms.openlocfilehash: 56ef4d9b75e8051a17c276556a321ed19ddcf2d8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a>外部 SMP SQL 伺服器設定為接收遠端資料表的副本
描述如何設定外部 SQL Server 執行個體從 SQL Server PDW 接收遠端資料表的複本。  
  
本主題說明設定遠端資料表複製的組態步驟的其中一個。 如需所有設定步驟，請參閱[遠端資料表複製](remote-table-copy.md)。  
  
## <a name="before-you-begin"></a>開始之前  
您可以設定外部的 SQL Server 之前，您必須：  
  
-   有與 SQL Server 2008 Enterprise Edition 或準備好安裝或已安裝較新版的 Windows 系統。 Windows 系統必須已經設定根據中的指示[設定外部 Windows 系統以接收遠端資料表複本使用 InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)。  
  
-   Windows 系統管理員帳戶設定 SQL Server 執行個體和 Windows 系統的能力。  
  
-   SQL Server 登入帳戶 （如果已安裝 SQL Server） 建立登入並授與目的地資料庫上的權限的能力。  
  
## <a name="HowToSQLServer"></a>外部 SMP SQL 伺服器設定為接收遠端資料表的副本  
遠端資料表複製功能會將資料表從 SQL Server PDW 應用裝置複製到執行 Windows 系統的外部 SMP SQL Server 資料庫。 設定外部 Windows 系統接收遠端資料表之後, 的下一個步驟是安裝和設定 Windows 系統上的 SQL Server。  
  
若要設定 SQL Server，請使用下列步驟：  
  
1.  Windows 系統上安裝 SQL Server 2008 Enterprise Edition 或更新版本。 這被指 SMP SQL Server。  
  
2.  設定為接受固定的 TCP 通訊埠上的 TCP/IP 連接的 SQL Server。 預設為停用此設定，並必須啟用才能允許連線到 SMP SQL Server 的 SQL Server PDW。  
  
3.  請停用 Windows 防火牆，或設定 SMP SQL Server TCP 連接埠，讓它能夠搭配啟用的 Windows 防火牆。  
  
4.  設定 SQL Server 以允許 SQL Server 驗證模式。 平行處理的資料匯出一律會使用 SQL Server 帳戶進行驗證。  
  
5.  判斷 SQL Server 上的帳戶將用於驗證 SMP SQL Server。 授與該帳戶的權限建立、 卸除，並將資料插入資料表平行處理資料匯出作業的目的地資料庫中。  
  
## <a name="BPSQLConfig"></a>遠端資料表複製的 SMP SQL Server 組態的最佳作法  
設定要接收遠端資料表複製 SMP SQL Server 時，使用下列最佳作法來改善效能。  
  
1.  SQL Server 產品文件中所述，請遵循最佳作法。 例如，啟用資料加密。 如需保護 SQL Server 的詳細資訊，請參閱[保護 SQL Server](../relational-databases/security/securing-sql-server.md) MSDN 上。  
  
2.  使用大量記錄或簡單復原模式。  
  
    平行處理資料期間匯出作業，資料會在大量插入至新建立的目的地資料表。 在大量插入期間的最大效能，設定目的地資料庫使用大量記錄或簡單復原模式。  
  
3.  若要回收記錄空間使用 batch_size 選項。  
  
    大量記錄或簡單復原模型使用最低限度記錄大量插入資料，雖然有些仍會進行記錄。 若要防止記錄檔變得太大，請使用 SQL Server batch_size 選項以定期回收記錄空間。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
