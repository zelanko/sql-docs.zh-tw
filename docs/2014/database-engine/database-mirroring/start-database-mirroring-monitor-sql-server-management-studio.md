---
title: 啟動資料庫鏡像監視器 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- Database Mirroring Monitor [SQL Server], starting
- database mirroring [SQL Server], monitoring
ms.assetid: 53165335-97ca-4f88-8e78-22f1839dee98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7a48c6620d4395cd44aac6f43cd1817cfebf785e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754903"
---
# <a name="start-database-mirroring-monitor-sql-server-management-studio"></a>啟動資料庫鏡像監視器 (SQL Server Management Studio)
  資料庫鏡像監視器是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監視器的一部分，是從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]啟動。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都可使用資料庫鏡像監視器。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
### <a name="to-launch-the-database-mirroring-monitor"></a>啟動資料庫鏡像監視器  
  
1.  連接到主體伺服器執行個體後，在 [物件總管] 中按一下伺服器名稱，以展開伺服器樹狀目錄。  
  
2.  展開 [資料庫]  ，然後選取要監視的資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，選取 [工作]  ，再按一下 [啟動資料庫鏡像監視器]  。  
  
4.  在 [資料庫鏡像監視器]  對話方塊中，按一下 [註冊鏡像資料庫]  以註冊一或多個鏡像資料庫。  
  
    > [!NOTE]  
    >  當您在某個夥伴註冊資料庫時，就會在另一個夥伴自動註冊資料庫。 如果監視器已經有其他夥伴執行個體的連接認證時，就會使用這些認證進行連接， 否則監視器會嘗試使用 Windows 驗證進行連接。 如果您想要變更用來連接至任一伺服器執行個體的認證，請按一下 [當我按一下確定時，即顯示管理伺服器連接對話方塊]  。  
  
 如需資料庫鏡像監視器的詳細資訊，請參閱[資料庫鏡像監視器概觀](database-mirroring-monitor-overview.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
  
