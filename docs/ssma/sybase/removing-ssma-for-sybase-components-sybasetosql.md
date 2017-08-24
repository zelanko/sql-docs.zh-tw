---
title: "移除 SSMA for Sybase 元件 (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bd57909a4aade0a07da76f0e222fb21e58e643c3
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>移除 SSMA for Sybase 元件 (SybaseToSQL)
當您完成將資料庫移轉從 Sybase Adaptive Server Enterprise (ASE) 至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可能想要解除安裝 SSMA 元件。 您可以在任何時候，解除安裝用戶端元件，但您不應該解除安裝的延伸模組組件，從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]除非您確定您已移轉的資料庫不再使用中的函式**ssma_syb**的結構描述**sysdb**資料庫。  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>正在 SSMA for Sybase 用戶端解除安裝  
您可以使用解除安裝 SSMA**新增或移除程式**。  
  
**若要解除安裝 SSMA**  
  
1.  在控制台中開啟**新增或移除程式**。  
  
2.  選取**Microsoft SQL Server 移轉小幫手 for Sybase**，然後按一下 **移除**。  
  
3.  若要確認您想要解除安裝 SSMA，請按一下**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>解除安裝延伸模組組件  
如果您確定您已移轉的資料庫不會使用中的物件**sysdb.ssma_syb**結構描述中，您可以使用來移除延伸模組組件**新增或移除程式**。  
  
若要解除安裝延伸模組組件  
  
1.  在控制台中開啟**新增或移除程式**。  
  
2.  選取**Microsoft SQL Server 移轉小幫手 Sybase 延伸模組組件的**，然後按一下 **移除**。  
  
3.  若要確認您想要解除安裝延伸模組組件，請按一下**是**。  
  
4.  在執行個體的公用程式資料庫的指令碼頁面上，按一下 **下一步**。  
  
5.  在 [連接參數] 頁面上選取驗證方法，然後**下一步**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入 SQL Server 執行個體。 如果您選取 SQL Server 驗證時，您必須輸入的 SQL Server 登入名稱和密碼。  
  
6.  在完成作業] 頁面上，按一下 [**確定**。  
  
7.  在完成] 5d; 頁面上，按一下 [**結束**。  
  
解除安裝之後，您可以確認**sysdb.ssma_syb**結構描述，以及可能是整個**sysdb**資料庫中，已移除使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。 不過，如果您使用其他 SSMA 產品時，他們也使用**sysdb**資料庫。 如果資料庫存在，而且確定沒有其他資料庫參考在此資料庫中的物件，您可以卸離資料庫。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Sybase 用戶端 &#40;SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[在 SQL Server &#40; 安裝 SSMA 元件SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  

