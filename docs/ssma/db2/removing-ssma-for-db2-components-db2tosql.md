---
title: 移除 SSMA for DB2 元件 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d4f819a92885cf5d173bcdda53ebf3291c958eac
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52520956"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>移除 SSMA for DB2 元件 (DB2ToSQL)
當您完成從 DB2，以便將資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可能想要解除安裝 SSMA 元件。 您可以在任何時間，以解除安裝用戶端元件。 不過，您不應該解除安裝延伸模組套件，從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]除非您已移轉的資料庫不再使用中的函式**ssma_DB2**的結構描述**sysdb**資料庫。  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>正在 SSMA for DB2 用戶端解除安裝  
您可以使用連線，解除安裝 SSMA**新增或移除程式**。  
  
**若要解除安裝 SSMA**  
  
1.  在控制台中，開啟**新增或移除程式**。  
  
2.  選取**[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手 for DB2**，然後按一下 **移除**。  
  
3.  若要確認您想要解除安裝 SSMA，請按一下**是**。  
  
## <a name="uninstalling-the-extension-pack"></a>解除安裝延伸模組組件  
如果您確定您已移轉的資料庫不會使用中的物件**sysdb.ssma_DB2**結構描述中，您可以藉由刪除從結構描述中移除延伸模組組件-沒有任何 Windows 解除安裝  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for DB2 用戶端&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[SQL Server 上安裝 SSMA 元件&#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
