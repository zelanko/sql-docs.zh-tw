---
title: 移除 SSMA for MySQL 元件（MySQLToSql） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3a5d6d1234cc294cc8e8cdd163ce8a9bd6ac3e3f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67929389"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>移除 SSMA for MySQL 元件 (MySQLToSql)
當您完成將資料庫從 MySQL 遷移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，您可能會想要卸載 SSMA 元件。 您可以隨時卸載用戶端元件。 不過，如果您從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]卸載延伸模組套件，則 SSMA 將不再支援使用伺服器端資料移轉引擎，從 MySQL 將資料移轉至目標資料庫（SQL SERVER/SQL Azure）。  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>卸載 SSMA for MySQL 用戶端  
您可以使用 [**新增或移除程式**] 來卸載 SSMA。  
  
**卸載 SSMA**  
  
1.  在 [控制台] 中，開啟 [新增或移除程式]。  
  
2.  選取 [**適用于 MySQL 的 Microsoft SQL Server 移轉小幫手**]，然後按一下 [**移除**]。  
  
3.  若要確認您想要卸載 SSMA，請按一下 **[是]**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸載擴充功能套件  
您可以使用 [**新增或移除程式**] 來移除延伸模組套件。  
  
**卸載擴充功能套件**  
  
1.  在 [控制台] 中，開啟 [新增或移除程式]。  
  
2.  選取 [**適用于 MySQL 延伸套件的 Microsoft SQL Server 移轉小幫手**]，然後按一下 [**移除**]。  
  
3.  若要確認您想要卸載延伸模組套件，請按一下 **[是]**。  
  
4.  在 [具有公用程式的實例資料庫腳本] 頁面上，選取實例，然後按 **[下一步]**。  
  
5.  在 [連接參數] 頁面上，選取驗證方法，然後按 **[下一步]**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入的實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [驗證]，則必須輸入登入名稱和密碼。  
  
6.  在 [操作已完成] 頁面上，按一下 **[確定]**。  
  
7.  在 [完成] 頁面上 **，按一下 [** 結束]。  
  
完成卸載程式之後，您可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來確認**ssma_MySQL sysdb**架構中的物件（可能是整個**sysdb**資料庫）已被移除。 不過，如果您使用其他 SSMA 產品，它們也會使用**sysdb**資料庫。 如果資料庫存在，而且您確定沒有其他資料庫參考此資料庫中的物件，則可以卸離資料庫。  
  
## <a name="see-also"></a>另請參閱  
[安裝適用于 MySQL 的 SSMA 用戶端 &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[在 SQL Server 上安裝 SSMA 元件](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
