---
title: '&lt;代理程式名稱&gt; 代理程式安全性 | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.agentnameagentsecurity.f1
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 039ec0c4401bc9748e1fa04fe89bcb69f055270c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "76288153"
---
# <a name="ltagentnamegt-agent-security"></a>&lt;AgentName&gt; 代理程式安全性
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [**代理程式名稱> 代理程式安全]\<** 頁面，可以讓您指定散發代理程式 (適用於交易式與快照式複寫) 或合併代理程式 (適用於合併式複寫) 用以執行並連接到複寫拓撲中之電腦的帳戶。 如需代理程式所需權限和複寫安全性最佳做法的資訊，請參閱[複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)和[複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
## <a name="options"></a>選項。  
 按一下每個訂閱者之資料列中的屬性按鈕 ( **...** )，即可存取 **[散發代理程式安全性]** 或 **[合併代理程式安全性]** 對話方塊。 如需有關代理程式所使用帳戶需要之權限的詳細資訊，請在所啟動之對話方塊上，按一下 **[說明]** 。  
  
 在其中的一個對話方塊中輸入設定之後，訂閱者的連接資訊就會在方格中顯示。  
  
 **訂閱者的代理程式**  
 每個訂閱者的名稱。  
  
 **散發者的連接**  
 這會針對交易式與快照式複寫顯示。 用於連接到散發者的內容。 本機連接一律會使用執行代理程式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的內容來進行：  
  
-   對於發送訂閱，本機連接會連接到散發者，所以此欄位一律會顯示：發送訂閱的 [模擬 '**網域>\<<登入\\']\>** 或是 [模擬 '**電腦>\<<登入\\']\>** 。  
  
-   針對提取訂閱，連線也可以用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的內容來進行。 欄位會顯示下列內容之一：[使用者登入 '**登入>']\<** 、[模擬 '**網域>\<<登入\\']\>** 或 [模擬 '**電腦>\<<登入\\']\>** 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議使用 Windows 帳戶的內容進行所有連接。  
  
 **發行者和散發者的連接**  
 這會針對合併複寫顯示。 連接到發行者與散發者所使用的內容。 本機連接一律會使用執行代理程式之 Windows 帳戶的內容進行連接：  
  
-   對於發送訂閱，本機連接會連接到發行者和散發者，所以此欄位一律會顯示：發送訂閱的 [模擬 '**網域>\<<登入\\']\>** 或是 [模擬 '**電腦>\<<登入\\']\>** 。  
  
-   對於提取訂閱，連接也可以用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的內容來進行。 欄位會顯示下列內容之一：[使用者登入 '**登入>']\<** 、[模擬 '**網域>\<<登入\\']\>** 或 [模擬 '**電腦>\<<登入\\']\>** 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議使用 Windows 帳戶的內容進行所有連接。  
  
 **訂閱者的連接**  
 與訂閱者進行連接的內容。 本機連接一律會使用執行代理程式之 Windows 帳戶的內容進行連接：  
  
-   對於提取訂閱，本機連接會連接到訂閱者，所以此欄位一律會顯示：發送訂閱的 [模擬 '**網域>\<<登入\\']\>** 或是 [模擬 '**電腦>\<<登入\\']\>** 。  
  
-   對於發送訂閱，連接也可以用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的內容來進行。 欄位會顯示下列內容之一：[使用者登入 '**登入>']\<** 、[模擬 '**網域>\<<登入\\']\>** 或 [模擬 '**電腦>\<<登入\\']\>** 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議使用 Windows 帳戶的內容進行所有連接。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [檢視及修改發送訂閱屬性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [用於複寫的身分識別和存取控制](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
