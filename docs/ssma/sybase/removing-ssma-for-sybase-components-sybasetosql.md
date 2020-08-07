---
title: " (SybaseToSQL) 移除 Sybase 元件的 SSMA |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4ffa47be1f35e86d09c136e5aeca6c0811630ca5
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87930549"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>移除 SSMA for Sybase 元件 (SybaseToSQL)
當您完成將資料庫從 Sybase 自動調整伺服器 Enterprise (ASE) 遷移到時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可能會想要卸載 SSMA 元件。 您可以隨時卸載用戶端元件，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 除非您確定遷移的資料庫不再使用**sysdb**資料庫的**ssma_syb**架構中的函式，否則不應從卸載擴充功能套件。  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>卸載 Sybase 用戶端的 SSMA  
您可以使用 [**新增或移除程式**] 來卸載 SSMA。  
  
**卸載 SSMA**  
  
1.  在 [控制台] 中，開啟 [新增或移除程式]。  
  
2.  選取 [ **Microsoft SQL Server 移轉小幫手用於 Sybase**]，然後按一下 [**移除**]。  
  
3.  若要確認您想要卸載 SSMA，請按一下 **[是]**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸載擴充功能套件  
如果您確定遷移的資料庫不使用**ssma_syb sysdb**架構中的物件，您可以使用 [**新增或移除程式**] 來移除延伸模組套件。  
  
卸載擴充功能套件  
  
1.  在 [控制台] 中，開啟 [新增或移除程式]。  
  
2.  選取 [Microsoft SQL Server 移轉小幫手] 做**為 [Sybase 延伸模組套件**]，然後按一下 [**移除**]。  
  
3.  若要確認您想要卸載延伸模組套件，請按一下 **[是]**。  
  
4.  在 [具有公用程式資料庫的實例腳本] 頁面上，按 **[下一步]**。  
  
5.  在 [連接參數] 頁面上，選取驗證方法，然後按 **[下一步]**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入 SQL Server 的實例。 如果您選取 [SQL Server 驗證]，則必須輸入 SQL Server 登入名稱和密碼。  
  
6.  在 [操作已完成] 頁面上，按一下 **[確定]**。  
  
7.  在 [完成] 頁面上 **，按一下 [** 結束]。  
  
卸載之後，您可以使用來確認**ssma_syb sysdb**架構（可能是整個**sysdb**資料庫）已被移除 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。 不過，如果您使用其他 SSMA 產品，它們也會使用**sysdb**資料庫。 如果資料庫存在，而且您確定沒有其他資料庫參考此資料庫中的物件，您可以卸離資料庫。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Sybase 用戶端 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[在 SQL Server &#40;SybaseToSQL 上安裝 SSMA 元件&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
