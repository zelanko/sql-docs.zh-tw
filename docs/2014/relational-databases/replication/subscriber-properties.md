---
title: 訂閱者屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3142a78fcf3a2413e43b1a7598b5d3b282aba1c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62629440"
---
# <a name="subscriber-properties"></a>訂閱者屬性
  [**訂閱者屬性**] 對話方塊包含執行之前[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]版本之訂閱者的相關資訊。  
  
## <a name="options"></a>選項。  
 **代理程式與訂閱者的連接**  
 散發代理程式和合併代理程式從散發者連接至訂閱者所用的內容。這個選項只適用於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以前的版本。  
  
 選取 **[模擬代理程式處理帳戶]** ，即可使用散發者端之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 帳戶的內容與訂閱者建立連接，或指定 **[SQL Server 驗證]**，然後輸入 **[登入]** 和 **[密碼]** 的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)]建議您選取 [模擬**代理程式處理帳戶**]。  
  
 若為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本，每個訂閱的連接資訊會在「新增訂閱精靈」中指定，而且可在 **[訂閱屬性]** 對話方塊中進行變更。  
  
 **預設代理程式排程**  
 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以前 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]版本的訂閱者在「新增訂閱精靈」中使用的預設排程。  
  
 **其他**  
 包含訂閱者和訂閱者類型上的資訊。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改散發者和發行者屬性](view-and-modify-distributor-and-publisher-properties.md)   

 [訂閱發行集](subscribe-to-publications.md)  
  
  
