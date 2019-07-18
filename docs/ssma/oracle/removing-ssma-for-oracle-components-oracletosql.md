---
title: 移除 SSMA for Oracle 元件 (OracleToSQL) |Microsoft Docs
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
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266557"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>移除 SSMA for Oracle 元件 (OracleToSQL)
當您完成從 Oracle 資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可能想要解除安裝 SSMA 元件。 您可以在任何時間，以解除安裝用戶端元件。 不過，您不應該解除安裝延伸模組套件，從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非您已移轉的資料庫不再使用中的函式**ssma_oracle**的結構描述**sysdb**資料庫。  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>解除安裝 Oracle 用戶端的 SSMA  
您可以使用連線，解除安裝 SSMA**新增或移除程式**。  
  
**若要解除安裝 SSMA**  
  
1.  在控制台中，開啟**新增或移除程式**。  
  
2.  選取   **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for Oracle**，然後按一下**移除**。  
  
3.  若要確認您想要解除安裝 SSMA，請按一下**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>解除安裝延伸模組組件  
如果您確定您已移轉的資料庫不會使用中的物件**sysdb.ssma_oracle**結構描述中，您可以使用來移除延伸模組套件**新增或移除程式**。  
  
**若要解除安裝延伸模組套件**  
  
1.  在控制台中，開啟**新增或移除程式**。  
  
2.  選取  **Microsoft SQL Server Migration Assistant for Oracle 延伸模組組件**，然後按一下**移除**。  
  
3.  若要確認您想要解除安裝延伸模組組件，請按一下**是**。  
  
4.  在 公用程式資料庫指令碼頁面的執行個體，請選取執行個體，然後按一下 **下一步**。  
  
5.  在 [連接參數] 頁面中，選取驗證方法，，然後按一下 [**下一步]** 。  
  
    Windows 驗證將用來嘗試登入的執行個體的 Windows 認證[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，您必須輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入名稱和密碼。  
  
6.  在完成作業 頁面上，按一下**確定**。  
  
7.  在 完成 頁面上，按一下 **結束**。  
  
在解除安裝之後, 您可以確認物件中**sysdb.ssma_oracle**結構描述，以及可能是整個**sysdb**資料庫中，已移除使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 不過，如果您使用其他的 SSMA 產品時，他們也使用**sysdb**資料庫。 如果資料庫存在，而且您會確定沒有其他的資料庫參考在此資料庫中的物件，您可以卸離資料庫。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Oracle 用戶端&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[SQL Server 上安裝 SSMA 元件&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
