---
title: "移除 SSMA for DB2 元件 (DB2ToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef9a64e458d03a0832ef3d5cd656747360e4a2db
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>移除 SSMA for DB2 元件 (DB2ToSQL)
當您完成將資料庫移轉至 DB2 從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您可能想要解除安裝 SSMA 元件。 您可以在任何時間，以解除安裝用戶端元件。 不過，您不應該解除安裝的延伸模組組件，從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]除非您已移轉的資料庫不再使用中的函式**ssma_DB2**的結構描述**sysdb**資料庫。  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>解除安裝的 DB2 用戶端的 SSMA  
您可以使用解除安裝 SSMA**新增或移除程式**。  
  
**若要解除安裝 SSMA**  
  
1.  在控制台中開啟**新增或移除程式**。  
  
2.  選取**[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手 for DB2**，然後按一下 **移除**。  
  
3.  若要確認您想要解除安裝 SSMA，請按一下**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>解除安裝延伸模組組件  
如果您確定您已移轉的資料庫不會使用中的物件**sysdb.ssma_DB2**結構描述中，您可以藉由刪除從結構描述中移除延伸模組組件 – 沒有任何 Windows 解除安裝  
  
## <a name="see-also"></a>請參閱  
[SSMA 安裝 DB2 用戶端 &#40; DB2ToSQL &#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[SSMA 元件安裝 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
