---
title: 取消隱藏執行自訂報表警告 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0829c079945c765efd836b25f30a54777c324a2a
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814374"
---
# <a name="unsuppress-run-custom-report-warnings"></a>取消隱藏執行自訂報表警告
  自訂報表有兩個警告對話方塊。 此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中取消隱藏這些方塊的顯示。  
  
 根據預設，[執行自訂報表] 對話方塊會在自訂報表執行之前顯示。 如果您選取了 [請不要再顯示這個警告] 核取方塊，將不再顯示此對話方塊。 此外，根據預設，當您開啟自訂報表，然後按一下連結來開啟另一份自訂報表時，就會顯示 [執行自訂報表] 對話方塊。 此對話方塊會顯示鑽研自訂報表檔案的完整路徑。 如果您選取了 [請不要再顯示這個警告] 核取方塊，將不再顯示此對話方塊。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>取消隱藏主要自訂報表警告對話方塊  
  
1.  連接到\<*伺服器*>\\<*共用*>|\<*磁碟機*> \Documents and Settings\\< UserProfile\>data\microsoft\microsoft SQL Server\120\Tools\Shell\reports.xml。  
  
2.  以滑鼠右鍵按一下`reports.xml`，然後按一下**編輯**。  
  
3.  變更**\<suppresswarning> 變更 >，則為 true\</SuppressWarning > 要\<suppresswarning> 變更 > false\</SuppressWarning >**。  
  
4.  重新啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>取消隱藏鑽研自訂報表警告對話方塊  
  
1.  連接到\<*伺服器*>\\<*共用*>|\<*磁碟機*> \Documents and Settings\\< UserProfile\>data\microsoft\microsoft SQL Server\120\Tools\Shell\reports.xml。  
  
2.  以滑鼠右鍵按一下`reports.xml`，然後按一下**編輯**。  
  
3.  變更 **\<suppressdrillthroughwarning> 變更 >，則為 true\</SuppressDrillthroughWarning > 要\<Suppressdrillthroughwarning> > false\</SuppressDrillthroughWarning >**.  
  
4.  重新啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [Management Studio 中的自訂報表](custom-reports-in-management-studio.md)   
 [將自訂報表加入 Management Studio](add-a-custom-report-to-management-studio.md)   
 [使用自訂報表搭配物件總管節點屬性](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
