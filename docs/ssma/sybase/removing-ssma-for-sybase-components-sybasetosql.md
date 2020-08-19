---
description: 移除 SSMA for Sybase 元件 (SybaseToSQL)
title: 移除 SSMA for Sybase 元件 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4c4e0f94f5672c96972a3cf3f3d35255dce91208
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468814"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>移除 SSMA for Sybase 元件 (SybaseToSQL)
當您完成將資料庫從 Sybase 調適型 Server Enterprise (ASE) 至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可能會想要將 SSMA 元件卸載。 您可以隨時卸載用戶端元件，但您不應該從卸載延伸模組套件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 除非您確定已遷移的資料庫不再使用**sysdb**資料庫的**ssma_syb**架構中的函數。  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>卸載 SSMA for Sybase 用戶端  
您可以使用 [ **新增或移除程式**] 卸載 SSMA。  
  
**卸載 SSMA**  
  
1.  在 [控制台] 中，開啟 [新增或移除程式]。  
  
2.  選取 [ **適用于 Sybase 的 Microsoft SQL Server 移轉小幫手**]，然後按一下 [ **移除**]。  
  
3.  若要確認您想要卸載 SSMA，請按一下 **[是]**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸載延伸模組套件  
如果您確定已遷移的資料庫未使用 **ssma_syb sysdb** 中的物件，您可以使用 [ **新增或移除程式**] 移除擴充功能套件。  
  
卸載擴充功能套件  
  
1.  在 [控制台] 中，開啟 [新增或移除程式]。  
  
2.  選取 [ **Sybase Extension Pack Microsoft SQL Server 移轉小幫手**]，然後按一下 [ **移除**]。  
  
3.  若要確認您想要卸載延伸模組套件，請按一下 **[是]**。  
  
4.  在 [具有公用程式資料庫腳本的實例] 頁面上，按 **[下一步]**。  
  
5.  在 [連接參數] 頁面上，選取驗證方法，然後按 **[下一步]**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入 SQL Server 的實例。 如果您選取 SQL Server 驗證，則必須輸入 SQL Server 登入名稱和密碼。  
  
6.  在 [作業已完成] 頁面上，按一下 **[確定]**。  
  
7.  在 [完成] 頁面上 **，按一下 [** 結束]。  
  
卸載之後，您可以使用來確認 **ssma_syb sysdb** 架構（可能是整個 **sysdb** 資料庫）已被移除 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。 但是，如果您使用其他 SSMA 產品，它們也會使用 **sysdb** 資料庫。 如果資料庫存在，而且您確定沒有其他資料庫參考此資料庫中的物件，您可以卸離資料庫。  
  
## <a name="see-also"></a>另請參閱  
[安裝適用于 Sybase 用戶端的 SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[在 SQL Server &#40;SybaseToSQL&#41;上安裝 SSMA 元件 ](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
