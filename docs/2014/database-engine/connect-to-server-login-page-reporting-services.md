---
title: 連線到伺服器 (登入頁面) Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.connecttors.login.f1
helpviewer_keywords:
- Connect to Server dialog box, Reporting Services
ms.assetid: d312c740-19d7-4931-84a2-88b805ec8439
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 468a462bac31bc731bab9e3ac815834fc614f57f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134785"
---
# <a name="connect-to-server-login-page-reporting-services"></a>連線到伺服器 (登入頁面) Reporting Services
  連線到 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 時，可使用此索引標籤檢視或指定下列選項。  
  
## <a name="options"></a>選項。  
 **伺服器類型**  
 從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從已註冊的伺服器註冊伺服器時，[伺服器類型] 方塊會呈現唯讀，並會與已註冊的伺服器元件中所顯示的伺服器類型進行比對。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [[!INCLUDE[ssDE](../includes/ssde-md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
 **伺服器名稱**  
 您要連接之報表伺服器執行個體的伺服器模式會決定您必須輸入的值。  
  
 若為以原生模式執行的報表伺服器，請指定要連接的報表伺服器執行個體。 如果您正使用預設執行個體，此伺服器名稱通常就是電腦的名稱。 如果您安裝具名執行個體，執行個體名稱附加至伺服器名稱，格式如下： \<servername >\\< InstanceName\>。 Reporting Services 會使用反斜線字元來分隔執行個體名稱。  
  
 若為以 SharePoint 整合模式執行的報表伺服器，您就必須指定 SharePoint 網站。 您可以在網站集合中指定與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]整合的任何網站。 您所提供的 URL 必須包含 HTTP 或 HTTPS 前置詞。 您必須擁有存取 SharePoint 網站的權限，才能在 Management Studio 中連接至此網站。 您被指派的權限等級將會決定您可以檢視和管理的項目。 如需詳細資訊，請參閱[連接到 Management Studio 中的報表伺服器](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)。  
  
 **驗證**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 可設定為接受您所提供之自訂驗證延伸模組處理的 Windows 驗證要求或表單驗證要求。 連接到 Reporting Services 時，請選取下列其中一種驗證模式：  
  
 **Windows 驗證模式 (Windows 驗證)**  
 使用您的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 認證連接到報表伺服器執行個體。  
  
 **基本驗證**  
 如果您的 Reporting Services 安裝設定為使用基本驗證，請使用 [基本驗證] 來連接。  
  
 **表單驗證**  
 如果您的 Reporting Services 安裝設定為使用自訂驗證延伸模組，請使用 [表單驗證] 來連接。  
  
 **使用者名稱**  
 請輸入連接將使用的登入名稱。 唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能使用此選項。  
  
 **密碼**  
 請輸入使用者名稱的密碼。 唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能編輯此選項。  
  
 **記住密碼**  
 請儲存您輸入的密碼。 您必須按一下 [選項] 才會顯示此選項，而且只有在選取使用 [基本] 或 [表單驗證] 進行連線時，才可編輯此選項。  
  
 **[連接]**  
 連接到選取的伺服器。  
  
 **選項。**  
 顯示其他伺服器連接選項，例如記住密碼。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器資料庫連接&#40;SSRS 組態管理員&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [連接至 Management Studio 中的報表伺服器](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [報表伺服器的驗證](../reporting-services/security/authentication-with-the-report-server.md)  
  
  