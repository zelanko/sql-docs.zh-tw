---
title: 正在移除 SSMA for Oracle 元件（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 0434f88c46d14672c84f5f7939488a827b229e27
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266557"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>移除 SSMA for Oracle 元件 (OracleToSQL)
當您完成將資料庫從 Oracle 遷移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，您可能會想要卸載 SSMA 元件。 您可以隨時卸載用戶端元件。 不過，除非您已遷移的資料庫不再使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysdb**資料庫的**ssma_oracle**架構中的函式，否則您不應該從卸載擴充功能套件。  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>卸載 SSMA for Oracle 用戶端  
您可以使用 [**新增或移除程式**] 來卸載 SSMA。  
  
**卸載 SSMA**  
  
1.  在 [控制台] 中，開啟 ****[新增或移除程式]。  
  
2.  ** [!INCLUDE[msCoName](../../includes/msconame_md.md)]選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [移轉小幫手**] 做為 [Oracle]，然後按一下 [**移除**]。  
  
3.  若要確認您想要卸載 SSMA，請按一下 **[是]**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸載擴充功能套件  
如果您確定遷移的資料庫不使用**ssma_oracle sysdb**架構中的物件，您可以使用 [**新增或移除程式**] 來移除延伸模組套件。  
  
**卸載擴充功能套件**  
  
1.  在 [控制台] 中，開啟 ****[新增或移除程式]。  
  
2.  選取 [ **Microsoft SQL Server 移轉小幫手 Oracle 延伸模組套件**]，然後按一下 [**移除**]。  
  
3.  若要確認您想要卸載延伸模組套件，請按一下 **[是]**。  
  
4.  在 [具有公用程式的實例資料庫腳本] 頁面上，選取實例，然後按 **[下一步]**。  
  
5.  在 [連接參數] 頁面上，選取驗證方法，然後按 **[下一步]**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入的實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [驗證]，則必須輸入登入名稱和密碼。  
  
6.  在 [操作已完成] 頁面上，按一下 **[確定]**。  
  
7.  在 [完成] 頁面上 **，按一下 [** 結束]。  
  
卸載之後，您可以使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來確認**ssma_oracle sysdb**架構中的物件（可能是整個**sysdb**資料庫）已被移除。 不過，如果您使用其他 SSMA 產品，它們也會使用**sysdb**資料庫。 如果資料庫存在，而且您確定沒有其他資料庫參考此資料庫中的物件，您可以卸離資料庫。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[在 SQL Server &#40;OracleToSQL 上安裝 SSMA 元件&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
