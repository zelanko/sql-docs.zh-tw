---
title: 正在移除 SSMA for DB2 元件 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6e5d1cd88027dfa3fb4216c93ab4e660ddcc0dc9
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936655"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>移除 SSMA for DB2 元件 (DB2ToSQL) 
當您完成將資料庫從 DB2 遷移至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可能會想要卸載 SSMA 元件。 您可以隨時卸載用戶端元件。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 除非您已遷移的資料庫不再使用**sysdb**資料庫的**ssma_DB2**架構中的函式，否則您不應該從卸載擴充功能套件。  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>卸載 SSMA for DB2 用戶端  
您可以使用 [**新增或移除程式**] 來卸載 SSMA。  
  
**卸載 SSMA**  
  
1.  在 [控制台] 中，開啟 [新增或移除程式]。  
  
2.  選取 [ ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 for DB2**]，然後按一下 [**移除**]。  
  
3.  若要確認您想要卸載 SSMA，請按一下 **[是]**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸載擴充功能套件  
如果您確定遷移的資料庫未使用**ssma_DB2 sysdb**中的物件，您可以從架構中刪除延伸模組，藉此將它移除，但沒有 Windows 卸載  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for DB2 Client &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[在 SQL Server &#40;DB2ToSQL 上安裝 SSMA 元件&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
