---
title: "連接到伺服器 (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connection.login.reportserver.f1
ms.assetid: ef81b658-8eb5-4636-ac81-eead10cc7b9f
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f48f75a346c30a4a142a67e83949b7f420030726
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-reporting-services"></a>連接到伺服器 (Reporting Services)
連接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] 時，使用此對話方塊來檢視或指定選項。  
  
## <a name="options"></a>選項。  
**伺服器類型**  
從物件總管****註冊伺服器時，選取要連接的伺服器類型：[!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器]**** 註冊伺服器時，[伺服器類型]**** 方塊是唯讀的，且會與 [已註冊的伺服器]**** 元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器]**** 工具列中選取 [[!INCLUDE[ssDE](../../includes/ssde_md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
**伺服器名稱**  
您要連接之報表伺服器執行個體的伺服器模式會決定您必須輸入的值。  
  
若為以原生模式執行的報表伺服器，請指定要連接的報表伺服器執行個體。 如果您正使用預設執行個體，此伺服器名稱通常就是電腦的名稱。 您如有安裝具名執行個體，請使用下列格式，在伺服器名稱之前加上行個體名稱： <servername>\\<InstanceName>。 Reporting Services 會使用反斜線字元來分隔執行個體名稱。  
  
若為以 SharePoint 整合模式執行的報表伺服器，您就必須指定 SharePoint 網站。 您可以在網站集合中指定與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]整合的任何網站。 您所提供的 URL 必須包含 HTTP 或 HTTPS 前置詞。 您必須擁有存取 SharePoint 網站的權限，才能在 Management Studio 中連接至此網站。 您被指派的權限等級將會決定您可以檢視和管理的項目。 如需詳細資訊，請參閱 [如何：註冊及連接到報表伺服器](http://msdn.microsoft.com/en-us/c875ff87-ee7d-443a-a702-bdb4b6c27c6e)。  
  
**驗證**  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] 可設定為接受由您提供之自訂驗證延伸模組處理的 Windows 驗證要求或表單驗證要求。 連接到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]時，請選取下列其中一種驗證模式：  
  
**Windows 驗證模式 (Windows 驗證)**  
使用您的 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 認證連接到報表伺服器執行個體。  
  
**基本驗證**  
如果您的 Reporting Services 安裝設定為使用基本驗證，請使用 [基本驗證]**** 來連接。  
  
**表單驗證**  
如果您的 Reporting Services 安裝設定為使用自訂驗證延伸模組，請使用 [表單驗證]**** 來連接。  
  
**使用者名稱**  
請輸入連接將使用的登入名稱。 唯有選取 **[基本驗證]** 或 **[表單驗證]**時，才能使用此選項。  
  
**密碼**  
請輸入使用者名稱的密碼。 唯有選取 **[基本驗證]** 或 **[表單驗證]**時，才能編輯此選項。  
  
**連接**  
按一下即可連接到上列所選的伺服器。  
  
**選項。**  
按一下即可顯示其他伺服器連接選項，例如，註冊伺服器與記住密碼。  
  
## <a name="see-also"></a>另請參閱  
[設定報表伺服器連線](http://msdn.microsoft.com/en-us/9759a9fb-35e9-4215-969b-a9f1fea18487)  
[如何：註冊及連接到報表伺服器](http://msdn.microsoft.com/en-us/c875ff87-ee7d-443a-a702-bdb4b6c27c6e)  
[在 Reporting Services 中設定驗證](http://msdn.microsoft.com/en-us/753c2542-0e97-4d8f-a5dd-4b07a5cd10ab)  
  

