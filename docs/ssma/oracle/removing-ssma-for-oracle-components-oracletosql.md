---
title: 移除 SSMA for Oracle 元件 (OracleToSQL) |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 369c3d4cba7e60bde7c7f55bb1e96fd0d7ac4381
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>移除 SSMA for Oracle 元件 (OracleToSQL)
當您完成從 Oracle 資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可能想要解除安裝 SSMA 元件。 您可以在任何時間，以解除安裝用戶端元件。 不過，您不應該解除安裝的延伸模組組件，從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]除非您已移轉的資料庫不再使用中的函式**ssma_oracle**的結構描述**sysdb**資料庫。  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>解除安裝 Oracle 用戶端的 SSMA  
您可以使用解除安裝 SSMA**新增或移除程式**。  
  
**若要解除安裝 SSMA**  
  
1.  在控制台中開啟**新增或移除程式**。  
  
2.  選取 **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手]，Oracle**，然後按一下 [**移除**。  
  
3.  若要確認您想要解除安裝 SSMA，請按一下**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>解除安裝延伸模組組件  
如果您確定您已移轉的資料庫不會使用中的物件**sysdb.ssma_oracle**結構描述中，您可以使用來移除延伸模組組件**新增或移除程式**。  
  
**若要解除安裝延伸模組組件**  
  
1.  在控制台中開啟**新增或移除程式**。  
  
2.  選取**Microsoft SQL Server 移轉小幫手 Oracle 延伸模組組件的**，然後按一下 **移除**。  
  
3.  若要確認您想要解除安裝延伸模組組件，請按一下**是**。  
  
4.  公用程式資料庫的指令碼頁面的執行個體上, 選取的執行個體，然後按一下 **下一步**。  
  
5.  在 [連接參數] 頁面上選取驗證方法，然後**下一步**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證，您必須輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入名稱和密碼。  
  
6.  在完成作業] 頁面上，按一下 [**確定**。  
  
7.  在完成] 5d; 頁面上，按一下 [**結束**。  
  
解除安裝之後，您可以確認物件中**sysdb.ssma_oracle**結構描述，以及可能是整個**sysdb**資料庫中，已移除使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]。 不過，如果您使用其他 SSMA 產品時，他們也使用**sysdb**資料庫。 如果資料庫存在，而且確定沒有其他資料庫參考在此資料庫中的物件，您可以卸離資料庫。  
  
## <a name="see-also"></a>請參閱  
[SSMA 安裝 Oracle 用戶端 &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[SSMA 元件安裝 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
