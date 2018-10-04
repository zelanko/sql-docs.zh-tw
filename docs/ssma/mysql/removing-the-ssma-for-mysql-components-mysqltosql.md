---
title: 移除 SSMA for MySQL 元件 (MySQLToSql) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ad23c4add9b6e7ea9999a434261a95282f129935
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604847"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>移除 SSMA for MySQL 元件 (MySQLToSql)
當您完成移轉的資料庫從 mysql 移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可能想要解除安裝 SSMA 元件。 您可以在任何時間，以解除安裝用戶端元件。 不過，如果您解除安裝延伸模組套件，從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然後 SSMA 將不再支援從 MySQL 到目標資料庫 (SQL Server/SQL Azure)，使用伺服器端資料移轉引擎中的資料移轉。  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>正在 SSMA for MySQL 用戶端解除安裝  
您可以使用連線，解除安裝 SSMA**新增或移除程式**。  
  
**若要解除安裝 SSMA**  
  
1.  在控制台中，開啟**新增或移除程式**。  
  
2.  選取  **Microsoft SQL Server Migration Assistant for MySQL**，然後按一下**移除**。  
  
3.  若要確認您想要解除安裝 SSMA，請按一下**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>解除安裝延伸模組組件  
您可以使用來移除延伸模組套件**新增或移除程式**。  
  
**若要解除安裝延伸模組套件**  
  
1.  在控制台中，開啟**新增或移除程式**。  
  
2.  選取  **Microsoft SQL Server Migration Assistant for MySQL 擴充功能套件**，然後按一下**移除**。  
  
3.  若要確認您想要解除安裝延伸模組組件，請按一下**是**。  
  
4.  在 公用程式資料庫指令碼頁面的執行個體，請選取執行個體，然後按一下 **下一步**。  
  
5.  在 [連接參數] 頁面中，選取驗證方法，，然後按一下 [**下一步]**。  
  
    Windows 驗證將用來嘗試登入的執行個體的 Windows 認證[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，您必須輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入名稱和密碼。  
  
6.  在完成作業 頁面上，按一下**確定**。  
  
7.  在 完成 頁面上，按一下 **結束**。  
  
解除安裝程序完成之後，您可以確認物件中**sysdb.ssma_MySQL**結構描述，以及可能是整個**sysdb**資料庫中，已移除使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 不過，如果您使用其他的 SSMA 產品時，他們也使用**sysdb**資料庫。 如果此資料庫確實存在，而且您已確定此資料庫中的物件參考的其他資料庫，您可以卸離資料庫。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for MySQL 用戶端&#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[在 SQL Server 上安裝 SSMA 元件](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
