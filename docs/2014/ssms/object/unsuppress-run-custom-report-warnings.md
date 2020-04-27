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
manager: craigg
ms.openlocfilehash: ed653b16fe524f364ba89f13e00715b725080033
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62824389"
---
# <a name="unsuppress-run-custom-report-warnings"></a>取消隱藏執行自訂報表警告
  自訂報表有兩個警告對話方塊。 此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中取消隱藏這些方塊的顯示。  
  
 根據預設，[執行自訂報表]  對話方塊會在自訂報表執行之前顯示。 如果您選取了 [請不要再顯示這個警告]  核取方塊，將不再顯示此對話方塊。 此外，根據預設，當您開啟自訂報表，然後按一下連結來開啟另一份自訂報表時，就會顯示 [執行自訂報表]  對話方塊。 此對話方塊會顯示鑽研自訂報表檔案的完整路徑。 如果您選取了 [請不要再顯示這個警告]  核取方塊，將不再顯示此對話方塊。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>取消隱藏主要自訂報表警告對話方塊  
  
1.  連接到\<*伺服器*> \\ \< * * \\ \>*共用*磁片磁碟機> \documents 和設定<UserProfile \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.>| <  
  
2.  按一下`reports.xml`滑鼠右鍵，然後按一下 [**編輯**]。  
  
3.  將**\<suppresswarning>>true\</SuppressWarning> 變更\<為 suppresswarning>>\<false/SuppressWarning>**。  
  
4.  重新啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>取消隱藏鑽研自訂報表警告對話方塊  
  
1.  連接到\<*伺服器*> \\ \< * * \\ \>*共用*磁片磁碟機> \documents 和設定<UserProfile \Application Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.>| <  
  
2.  按一下`reports.xml`滑鼠右鍵，然後按一下 [**編輯**]。  
  
3.  將** \<suppressdrillthroughwarning>>true\</SuppressDrillthroughWarning>變更\<為 suppressdrillthroughwarning>>\<false/SuppressDrillthroughWarning>**。  
  
4.  重新啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [Management Studio 中的自訂報表](custom-reports-in-management-studio.md)   
 [將自訂報表加入至 Management Studio](add-a-custom-report-to-management-studio.md)   
 [使用自訂報表搭配物件總管節點屬性](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
