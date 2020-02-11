---
title: 新增或編輯服務器註冊（一般索引標籤）（Reporting Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerserver.general.reportserver.f1
ms.assetid: 5f899a8e-52ef-46b5-b7a9-f200ccd9f724
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0e6d6d3ad57726c42556c9ecc2662edce102e57
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62844264"
---
# <a name="new-or-edit-server-registration-general-tab-reporting-services"></a>新增或編輯伺服器註冊 (一般索引標籤) (Reporting Services)
  當您註冊 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的執行個體時，請使用此索引標籤來指定選項。  
  
 若要存取此頁面，請在 [已註冊的伺服器]**** 工具列按一下 [Reporting Services]****，以滑鼠右鍵按一下任何已註冊的伺服器群組 (例如 [Reporting Services]****)，指向 [新增]****，然後按一下 [伺服器註冊]****。  
  
## <a name="options"></a>選項。  
 **伺服器類型**  
 從 [已註冊的伺服器] 註冊伺服器時，[**伺服器類型**] 方塊是唯讀的，而且會與 [**已註冊的伺服器**] 窗格中顯示的伺服器類型相符。 若要註冊一個不同類型的伺服器，在開始註冊新伺服器之前，請在 **[已註冊的伺服器]** 工具列上按一下您想要的伺服器。  
  
 **伺服器名稱**  
 指定要連接到的報表伺服器執行個體。 在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]中，您可以透過執行個體名稱來存取報表伺服器。 您安裝的每一個 SQL Server 執行個體可以有一個報表伺服器執行個體。 如果您使用預設執行個體，請鍵入 SQL Server 執行個體的名稱。 如果您使用具名執行個體，請以 MSSQL$InstanceName 格式指定要連接到報表伺服器的具名執行個體。  
  
 **驗證**  
 對報表伺服器的驗證是透過 Internet Information Services (IIS) 來完成。 連接到 Reporting Services 時，請選取下列其中一種驗證模式：  
  
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
 請儲存您輸入的密碼。 唯有已按一下 **[基本驗證]** 或 **[表單驗證]** 時，才能使用此選項。  
  
> [!NOTE]  
>  如果您已儲存密碼而想要停止儲存，請清除此核取方塊，然後按一下 [**儲存**]。  
  
 **已註冊的伺服器名稱**  
 您要在 [已註冊的伺服器] 上顯示的名稱。 此名稱不需與 **[伺服器名稱]** 方塊中的名稱相符。  
  
 **已註冊的伺服器描述**  
 輸入伺服器的選擇性描述。  
  
 **測驗**  
 按一下以測試與 [伺服器名稱]**** 中選取之伺服器的連接。  
  
 **另**  
 按一下即可儲存已註冊的伺服器設定。  
  
  
