---
title: 已註冊的伺服器 F1 說明
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], Help
- Registered Servers [SQL Server], help
- SQL Server Management Studio Help [SQL Server], registered servers
ms.assetid: 59f76b28-ba78-4a1a-b5d5-8b581f30114d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c011635e676cfc25cb4e5cc5acf357b11700080e
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011112"
---
# <a name="registered-servers-f1-help"></a>已註冊的伺服器 F1 說明
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  本節包含 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中 [已註冊的伺服器] 元件的 F1 說明。 它描述各種選項。
  
 若要了解已註冊的伺服器，並取得如何處理它們的連結，請移至 [註冊伺服器](../../tools/sql-server-management-studio/register-servers.md) 主題。 
 

 按一下即可儲存 [已註冊的伺服器] 設定。 
 
 ## <a name="reporting-services-new-or-edit-server-registration-general-tab"></a>Reporting Services 新增或編輯伺服器註冊 (一般索引標籤) 
  當您註冊 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的執行個體時，請使用此索引標籤來指定選項。  
  
 若要存取此頁面，請在 [已註冊的伺服器]  工具列按一下 [Reporting Services]  ，以滑鼠右鍵按一下任何已註冊的伺服器群組 (例如 [Reporting Services]  )，指向 [新增]  ，然後按一下 [伺服器註冊]  。  
  
### <a name="options"></a>選項。  
 **伺服器類型**  
 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型]  方塊是唯讀的，且會與 [已註冊的伺服器]  窗格中所顯示的伺服器類型相符。 若要註冊一個不同類型的伺服器，在開始註冊新伺服器之前，請在 **[已註冊的伺服器]** 工具列上按一下您想要的伺服器。  
  
 **伺服器名稱**  
 指定要連接到的報表伺服器執行個體。 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，您可以透過執行個體名稱來存取報表伺服器。 您安裝的每一個 SQL Server 執行個體可以有一個報表伺服器執行個體。 如果您使用預設執行個體，請鍵入 SQL Server 執行個體的名稱。 如果您使用具名執行個體，請以 MSSQL$InstanceName 格式指定要連接到報表伺服器的具名執行個體。  
  
 **驗證**  
 對報表伺服器的驗證是透過 Internet Information Services (IIS) 來完成。 連接到 Reporting Services 時，請選取下列其中一種驗證模式：  
  
 **Windows 驗證模式 (Windows 驗證)**  
 使用您的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認證連接到報表伺服器執行個體。  
  
 **基本驗證**  
 如果您的 Reporting Services 安裝設定為使用基本驗證，請使用 [基本驗證]  來連接。  
  
 **表單驗證**  
 如果您的 Reporting Services 安裝設定為使用自訂驗證延伸模組，請使用 [表單驗證]  來連接。  
  
 **使用者名稱**  
 請輸入連接將使用的登入名稱。 唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能使用此選項。  
  
 **密碼**  
 請輸入使用者名稱的密碼。 唯有選取 **[基本驗證]** 或 **[表單驗證]** 時，才能編輯此選項。  
  
 **記住密碼**  
 請儲存您輸入的密碼。 唯有已按一下 **[基本驗證]** 或 **[表單驗證]** 時，才能使用此選項。  
  
> **注意：** 如果您已儲存密碼而要停止儲存密碼，請清除此核取方塊，然後按一下 [儲存]  。  
  
 **已註冊的伺服器名稱**  
 您要在 [已註冊的伺服器] 上顯示的名稱。 此名稱不需與 **[伺服器名稱]** 方塊中的名稱相符。  
  
 **已註冊的伺服器描述**  
 輸入伺服器的選擇性描述。  
  
 **Test**  
 按一下以測試與 [伺服器名稱]  中選取之伺服器的連接。  
  
 
 ## <a name="analysis-services---multidimensional-data-new-or-edit-server-registration-general-tab"></a>Analysis Services - 多維度資料新增或編輯伺服器註冊 (一般索引標籤)
 
  當您註冊 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體時，請使用此索引標籤來指定選項。  
  
 若要存取這個頁面，請在 [已註冊的伺服器] 中按一下 [已註冊的伺服器] 工具列上的 [Analysis Services]  ，以滑鼠右鍵按一下任何已註冊的伺服器群組，例如 [Analysis Services]  ，並指向 [新增]  ，然後按一下 [伺服器註冊]  。  
  
### <a name="options"></a>選項。  
 **伺服器類型**  
 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型]  方塊是唯讀的，且會與 [已註冊的伺服器] 窗格中所顯示的伺服器類型相符。 若要註冊一個不同類型的伺服器，在開始註冊新伺服器之前，請在 **[已註冊的伺服器]** 工具列上按一下您想要的伺服器。  
  
 **伺服器名稱**  
 選取要連接的伺服器執行個體。 預設會顯示上次連接的伺服器執行個體。  
  
 **驗證**  
 Windows 驗證允許使用者使用其 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認證、以 Windows 使用者身分或是 Windows 群組成員的身分進行連接。  
  
 **使用者名稱**  
 這個選項在此版本中無法使用。  
  
 **密碼**  
 這個選項在此版本中無法使用。  
  
 **記住密碼**  
 這個選項在此版本中無法使用。  
  
 **已註冊的伺服器名稱**  
 您要在 [已註冊的伺服器] 上顯示的名稱。 此名稱不需要與 **[伺服器名稱]** 方塊中的名稱相符。  
  
 **已註冊的伺服器描述**  
 輸入伺服器的選擇性描述。  
  
 **Test**  
 按一下以測試與 [伺服器名稱]  中選取之伺服器的連接。 
 
 ## <a name="ssis-new-or-edit-server-registration-general-tab"></a>SSIS 新增或編輯伺服器註冊 (一般索引標籤) 
 
 註冊 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]時，使用這個索引標籤指定選項。  
  
 若要存取此頁面，請在 [已註冊的伺服器] 上按一下 [已註冊的伺服器] 工具列上的 [Integration Services]，並以滑鼠右鍵按一下任何已註冊的伺服器群組，再指向 [新增]，然後按一下 [伺服器註冊]。  
  
### <a name="options"></a>選項。  
 **伺服器類型**  
 在 [已註冊的伺服器] 中註冊伺服器時，[伺服器類型]  方塊是唯讀的，且會與 [已註冊的伺服器] 中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請在 [已註冊的伺服器]  工具列上按一下 **Database Engine**、**Analysis Server**、**Reporting Services**、**SQL Server Compact Edition**  或 **Integration Services**，然後才開始註冊新伺服器。  
  
 **伺服器名稱**  
 選取要連接的伺服器。 依預設，會顯示上次連接的伺服器。  
  
 **驗證**  
 Windows 驗證模式允許使用者透過 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者帳戶連接。  
  
 **使用者名稱**  
 這個選項在此版本中無法使用。  
  
 **密碼**  
 這個選項在此版本中無法使用。  
  
 **記住密碼**  
 這個選項在此版本中無法使用。  
  
 **已註冊的伺服器名稱**  
 您要在 [已註冊的伺服器]  上顯示的名稱。 此名稱不需要與 **[伺服器名稱]** 方塊中的名稱相符。  
  
 **已註冊的伺服器描述**  
 輸入伺服器的選擇性描述。  
  
 **Test**  
 按一下以測試與 [伺服器名稱]  中選取之伺服器的連接。 
  

 
 
  
