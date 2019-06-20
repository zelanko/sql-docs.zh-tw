---
title: 連接到伺服器 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connection.login.reportserver.f1
ms.assetid: ef81b658-8eb5-4636-ac81-eead10cc7b9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41e0ca3ee7ccaa7bb57e5667092c0660e35c4c52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62808675"
---
# <a name="connect-to-server-reporting-services"></a>連接到伺服器 (Reporting Services)
  連接到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 時，使用此對話方塊來檢視或指定選項。  
  
## <a name="options"></a>選項  
 **伺服器類型**  
 從物件總管  註冊伺服器時，選取要連接的伺服器類型：[!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器]  註冊伺服器時，[伺服器類型]  方塊是唯讀的，且會與 [已註冊的伺服器]  元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器]  工具列中選取 [[!INCLUDE[ssDE](../includes/ssde-md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
 **伺服器名稱**  
 您要連接之報表伺服器執行個體的伺服器模式會決定您必須輸入的值。  
  
 若為以原生模式執行的報表伺服器，請指定要連接的報表伺服器執行個體。 如果您正使用預設執行個體，此伺服器名稱通常就是電腦的名稱。 如果您已安裝具名執行個體，執行個體名稱附加至伺服器名稱，格式如下：\<伺服器名稱 >\\< 執行個體名稱\>。 Reporting Services 會使用反斜線字元來分隔執行個體名稱。  
  
 若為以 SharePoint 整合模式執行的報表伺服器，您就必須指定 SharePoint 網站。 您可以在網站集合中指定與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]整合的任何網站。 您所提供的 URL 必須包含 HTTP 或 HTTPS 前置詞。 您必須擁有存取 SharePoint 網站的權限，才能在 Management Studio 中連接至此網站。 您被指派的權限等級將會決定您可以檢視和管理的項目。 如需詳細資訊，請參閱 <<c0> [ 連接到 Management Studio 中的報表伺服器](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)。  
  
 **驗證**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 可設定為接受由您提供之自訂驗證延伸模組處理的 Windows 驗證要求或表單驗證要求。 連接到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]時，請選取下列其中一種驗證模式：  
  
 **Windows 驗證模式 (Windows 驗證)**  
 使用您的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 認證連接到報表伺服器執行個體。  
  
 **基本驗證**  
 如果您的 Reporting Services 安裝設定為使用基本驗證，請使用 [基本驗證]  來連接。  
  
 **表單驗證**  
 如果您的 Reporting Services 安裝設定為使用自訂驗證延伸模組，請使用 [表單驗證]  來連接。  
  
 **使用者名稱**  
 請輸入連接將使用的登入名稱。 唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能使用此選項。  
  
 **密碼**  
 請輸入使用者名稱的密碼。 唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能編輯此選項。  
  
 **[連接]**  
 按一下即可連接到上列所選的伺服器。  
  
 **選項。**  
 按一下即可顯示其他伺服器連接選項，例如，註冊伺服器與記住密碼。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [連接至 Management Studio 中的報表伺服器](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [報表伺服器的驗證](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
