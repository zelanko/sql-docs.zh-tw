---
title: "移除 SSMA for MySQL 元件 (MySQLToSql) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 765696847ddb1abd44dfac3463fdfd75f9a5c97a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>移除 SSMA for MySQL 元件 (MySQLToSql)
當您完成將資料庫移轉至 MySQL 從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可能想要解除安裝 SSMA 元件。 您可以在任何時間，以解除安裝用戶端元件。 不過，如果您解除安裝延伸模組組件從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，然後 SSMA 將不再支援使用伺服器端資料移轉引擎與目標資料庫 (SQL Server/SQL Azure) 的資料從 MySQL 移轉。  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>解除安裝 MySQL 用戶端的 SSMA  
您可以使用解除安裝 SSMA**新增或移除程式**。  
  
**若要解除安裝 SSMA**  
  
1.  在控制台中開啟**新增或移除程式**。  
  
2.  選取**Microsoft SQL Server 移轉小幫手的 MySQL**，然後按一下 **移除**。  
  
3.  若要確認您想要解除安裝 SSMA，請按一下**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>解除安裝延伸模組組件  
您可以使用來移除延伸模組組件**新增或移除程式**。  
  
**若要解除安裝延伸模組組件**  
  
1.  在控制台中開啟**新增或移除程式**。  
  
2.  選取**Microsoft SQL Server 移轉小幫手 MySQL 擴充功能組件的**，然後按一下 **移除**。  
  
3.  若要確認您想要解除安裝延伸模組組件，請按一下**是**。  
  
4.  公用程式資料庫的指令碼頁面的執行個體上, 選取的執行個體，然後按一下 **下一步**。  
  
5.  在 [連接參數] 頁面上選取驗證方法，然後**下一步**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證，您必須輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入名稱和密碼。  
  
6.  在完成作業] 頁面上，按一下 [**確定**。  
  
7.  在完成] 5d; 頁面上，按一下 [**結束**。  
  
解除安裝程序完成之後，您可以確認物件中**sysdb.ssma_MySQL**結構描述，以及可能是整個**sysdb**資料庫中，已移除使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。 不過，如果您使用其他 SSMA 產品時，他們也使用**sysdb**資料庫。 如果資料庫存在，而且您會確定沒有其他的資料庫參考的物件，此資料庫中，您可以卸離資料庫。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for MySQL 用戶端 &#40;MySQLToSQL &#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[安裝 SQL Server 上的 SSMA 元件](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  

