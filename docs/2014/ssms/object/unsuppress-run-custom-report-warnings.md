---
title: 取消隱藏執行自訂報表警告 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
author: stevestein
ms.author: sstein
ms.openlocfilehash: ae7f4d08ac613113d715728a5cb78ae37bd6f99b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058529"
---
# <a name="unsuppress-run-custom-report-warnings"></a>取消隱藏執行自訂報表警告
  自訂報表有兩個警告對話方塊。 此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中取消隱藏這些方塊的顯示。  
  
 根據預設，[執行自訂報表]  對話方塊會在自訂報表執行之前顯示。 如果您選取了 [請不要再顯示這個警告]  核取方塊，將不再顯示此對話方塊。 此外，根據預設，當您開啟自訂報表，然後按一下連結來開啟另一份自訂報表時，就會顯示 [執行自訂報表]  對話方塊。 此對話方塊會顯示鑽研自訂報表檔案的完整路徑。 如果您選取了 [請不要再顯示這個警告]  核取方塊，將不再顯示此對話方塊。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>取消隱藏主要自訂報表警告對話方塊  
  
1.  連接至 \<*Server*> \\ < *共用* >| \<*Drive*> \Documents 和設定 \\<UserProfile \> \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml。  
  
2.  按一下滑鼠右鍵 `reports.xml` ，然後按一下 [**編輯**]。  
  
3.  將** \<SuppressWarning> true \</SuppressWarning> 變更 \<SuppressWarning> 為 \</SuppressWarning> false**。  
  
4.  重新啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>取消隱藏鑽研自訂報表警告對話方塊  
  
1.  連接至 \<*Server*> \\ < *共用* >| \<*Drive*> \Documents 和設定 \\<UserProfile \> \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml。  
  
2.  按一下滑鼠右鍵 `reports.xml` ，然後按一下 [**編輯**]。  
  
3.  將** \<SuppressDrillthroughWarning> true \</SuppressDrillthroughWarning> 變更 \<SuppressDrillthroughWarning> 為 \</SuppressDrillthroughWarning> false**。  
  
4.  重新啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [Management Studio 中的自訂報表](custom-reports-in-management-studio.md)   
 [將自訂報表加入至 Management Studio](add-a-custom-report-to-management-studio.md)   
 [使用自訂報表搭配物件總管節點屬性](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
