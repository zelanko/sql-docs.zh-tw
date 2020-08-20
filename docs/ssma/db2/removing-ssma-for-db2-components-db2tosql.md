---
description: '移除 SSMA for DB2 元件 (DB2ToSQL) '
title: 移除 SSMA for DB2 元件 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0341869ff5d39ad35fce6ac450d293eaac1feb38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488165"
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>移除 SSMA for DB2 元件 (DB2ToSQL) 
當您完成將資料庫從 DB2 遷移至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可能會想要將 SSMA 元件卸載。 您可以隨時卸載用戶端元件。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 除非您已遷移的資料庫不再使用**sysdb**資料庫的**ssma_DB2**架構中的函式，否則您不應該從卸載擴充功能套件。  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>卸載 SSMA for DB2 用戶端  
您可以使用 [ **新增或移除程式**] 卸載 SSMA。  
  
**卸載 SSMA**  
  
1.  在 [控制台] 中，開啟 [新增或移除程式]。  
  
2.  選取 [ ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2 Migration Assistant**]，然後按一下 [**移除**]。  
  
3.  若要確認您想要卸載 SSMA，請按一下 **[是]**。  
  
## <a name="uninstalling-the-extension-pack"></a>卸載延伸模組套件  
如果您確定已遷移的資料庫未使用 **ssma_DB2 sysdb** 中的物件，您可以從架構中刪除擴充功能套件，也就是沒有 Windows 卸載  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for DB2 用戶端 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[在 SQL Server &#40;DB2ToSQL&#41;上安裝 SSMA 元件 ](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
