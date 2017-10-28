---
title: "變更已註冊之伺服器或已註冊之伺服器群組的名稱 | Microsoft Docs"
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying registered server or server group names
- server groups [SQL Server]
- Registered Servers [SQL Server], names
- renaming registered server or server group
- names [SQL Server], registered server or server group
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: b99eea0ee5988ce791948c2fa7340271b74e7ec4
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>變更已註冊之伺服器或已註冊之伺服器群組的名稱
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 變更 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中已註冊伺服器或伺服器群組的名稱。 該名稱可以隨時變更。 在「已註冊的伺服器」中變更伺服器名稱，僅會變更所顯示的名稱。 若要連接到其他伺服器，您必須編輯已註冊伺服器的連接屬性。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
從功能表，巡覽至 [檢視]\\[已註冊的伺服器] 開啟 [已註冊的伺服器] 窗格。  
#### <a name="to-change-the-name-of-a-server"></a>變更伺服器的名稱  
  
1.  在 [已註冊的伺服器] 中，依序展開 [資料庫引擎] 和 [本機伺服器群組]。  

2.  以滑鼠右鍵按一下伺服器，然後選取 [屬性] 開啟 [編輯伺服器註冊屬性] 對話方塊視窗。
  
3.  在 [已註冊的伺服器名稱] 文字方塊中，輸入伺服器註冊的新名稱，然後按一下 [儲存]。  
  
#### <a name="to-change-the-name-of-a-server-group"></a>若要變更伺服器群組名稱  
  
1.  在 [已註冊的伺服器] 中，依序展開 [資料庫引擎] 和 [本機伺服器群組]。  

2.  以滑鼠右鍵按一下伺服器群組，然後選取 [屬性] 開啟 [編輯伺服器群組屬性] 對話方塊視窗。 
  
3.  在 [群組名稱] 文字方塊中，輸入伺服器群組的新名稱，然後按一下 [儲存]。  
  
## <a name="see-also"></a>另請參閱  
 [變更伺服器的註冊 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)  
  
  

