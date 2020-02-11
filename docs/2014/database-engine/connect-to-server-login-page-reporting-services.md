---
title: 連線到伺服器 (登入頁面) Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttors.login.f1
helpviewer_keywords:
- Connect to Server dialog box, Reporting Services
ms.assetid: d312c740-19d7-4931-84a2-88b805ec8439
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7369e9d37e5f706786410f8e171c89c6c38287d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62808720"
---
# <a name="connect-to-server-login-page-reporting-services"></a>連線到伺服器 (登入頁面) Reporting Services
  連接到[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]時，使用此索引標籤來查看或指定下列選項。  
  
## <a name="options"></a>選項。  
 **伺服器類型**  
 從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型]**** 方塊是唯讀的，且會與 [已註冊的伺服器] 元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [[!INCLUDE[ssDE](../includes/ssde-md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
 **伺服器名稱**  
 您要連接之報表伺服器執行個體的伺服器模式會決定您必須輸入的值。  
  
 若為以原生模式執行的報表伺服器，請指定要連接的報表伺服器執行個體。 如果您正使用預設執行個體，此伺服器名稱通常就是電腦的名稱。 如果您安裝了已命名的實例，請使用下列格式將實例名稱附加到伺服器\<名稱： \\ servername>\><InstanceName。 Reporting Services 會使用反斜線字元來分隔執行個體名稱。  
  
 若為以 SharePoint 整合模式執行的報表伺服器，您就必須指定 SharePoint 網站。 您可以在網站集合中指定與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]整合的任何網站。 您所提供的 URL 必須包含 HTTP 或 HTTPS 前置詞。 您必須擁有存取 SharePoint 網站的權限，才能在 Management Studio 中連接至此網站。 您被指派的權限等級將會決定您可以檢視和管理的項目。 如需詳細資訊，請參閱 [Connect to a Report Server in Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md) (連線至 Management Studio 中的報表伺服器)。  
  
 **驗證**  
 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 可設定為接受由您提供之自訂驗證延伸模組處理的 Windows 驗證要求或表單驗證要求。 連接到 Reporting Services 時，請選取下列其中一種驗證模式：  
  
 **Windows 驗證模式（Windows 驗證）**  
 使用您的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 認證連接到報表伺服器執行個體。  
  
 **基本驗證**  
 如果您的 Reporting Services 安裝設定為使用基本驗證，請使用 [基本驗證]**** 來連接。  
  
 **表單驗證**  
 如果您的 Reporting Services 安裝設定為使用自訂驗證延伸模組，請使用 [表單驗證]**** 來連接。  
  
 **使用者名稱**  
 請輸入連接將使用的登入名稱。 唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能使用此選項。  
  
 **密碼**  
 輸入使用者名稱的密碼。 唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能編輯此選項。  
  
 **記住密碼**  
 請儲存您輸入的密碼。 您必須按一下 [選項]**** 才會顯示此選項，而且只有在選取使用 [基本]**** 或 [表單驗證]**** 進行連線時，才可編輯此選項。  
  
 **連線**  
 連接到選取的伺服器。  
  
 **選項**  
 顯示其他伺服器連接選項，例如記住密碼。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSRS Configuration Manager 設定報表伺服器資料庫連接&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [連接至 Management Studio 中的報表伺服器](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [報表伺服器的驗證](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
