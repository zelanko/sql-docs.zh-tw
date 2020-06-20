---
title: 接受授權條款 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 6d41879b84d98f72e570b00a61341a53d2e6187a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046445"
---
# <a name="accept-license-terms"></a>接受授權條款
  請使用 **安裝精靈的** [接受授權條款] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面來接受此版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的授權條款。  
  
 您可以列印授權合約，或將它複製到剪貼簿。 若要繼續，請接受授權條款，然後按 **[下一步]**。 若要結束安裝，請按一下 **[取消]**。  
  
## <a name="customer-experience-improvement-program-ceip"></a>客戶經驗改進計畫 (CEIP)  
 如果您啟用 CEIP 報表，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會設定為定期傳送報表至 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。 報表包含硬體組態及您如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和元件的相關資訊。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 將會使用功能使用方式資料來改進 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這項功能所監視的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件包括：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   複寫  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式  
  
 關於功能使用方式的資訊會傳送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)](以限制存取的方式予以儲存)。  
  
 若要在安裝程式完成之後停用 CEIP 報表，請使用 [組態工具] 功能表上的 [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤和使用方式報告**] 工具 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Configuration Tools** 。  
  
 對於安裝、升級、修復等等的安裝程式動作，僅會在執行安裝程式期間，收集並上傳資訊。  
  
 對於其他所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件，則會每天針對所有啟用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，收集一次資訊。 根據預設，收集的時間為午夜，好讓伺服器的負載減至最小。 如果您想要變更收集的時間，可手動編輯控制收集時間的登錄機碼。 每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體都擁有自己的登錄機碼：  
  
 HKLM\Software \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<INSTANCEID>\CPE\TimeofReporting  
  
 這個登錄機碼的值包含從 00:00 (午夜) 開始執行之收集時間的分鐘數。 例如，60 這個值會在 1:00 a.m. 執行收集，1200 這個值會在 8:00 p.m. 執行收集，以此類推。  
  
## <a name="error-reporting"></a>錯誤報告  
 使用 **安裝精靈的** [錯誤和使用方式報表設定] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面，可啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的功能錯誤和使用方式報告功能。  
  
### <a name="options"></a>選項  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]及其元件會停用功能使用方式資料收集和錯誤報告功能。  
  
 錯誤報告  
 如果您啟用錯誤報告功能，萬一下列任何一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件發生嚴重錯誤時， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 就會設定為自動將報表傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   複寫  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 使用錯誤報表來改進 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能，並將所有資訊視為機密資訊。  
  
 關於錯誤的資訊會透過安全 (https) 連接傳送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)](以限制存取的方式予以儲存)。 另外，錯誤報表也可以傳送到您自己的 Corporate Error Reporting 伺服器。  
  
 錯誤報表包含下列資訊：  
  
-   發生問題時的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 狀況。  
  
-   作業系統版本和電腦硬體資訊。  
  
-   數位產品識別碼，它不是用於識別授權。  
  
-   電腦或 Proxy 伺服器的網路 IP 位址。  
  
-   導致錯誤之處理序的記憶體或檔案中的資訊。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不刻意收集檔案、名稱、地址、電子郵件地址或任何形式的個人資訊。 不過，錯誤報表可包含導致錯誤之處理序的記憶體或檔案中的個人資訊。 雖然這項資訊可能用於判斷您的識別，但 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不會將這項資訊用於此用途。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 隱私權和資料收集原則的詳細資訊，請參閱 [Microsoft SQL Server 隱私權聲明](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md)。  
  
 如果您啟用錯誤報告卻發生嚴重錯誤，您可能會在 Windows 事件記錄檔中看到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的回應，它會指向關於特定錯誤的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫文件。  
  
 在安裝程式完成之後，若要對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有執行個體及其元件停用錯誤或功能使用方式報表，請到 **[錯誤和使用方式報表設定]** 對話方塊，清除 **[功能使用方式]** 的核取方塊。 如果**Error Reporting**已針對的多個元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （ [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和共用元件）啟用錯誤報表，您可以停用個別元件的每個實例和共用元件的錯誤報表（列為**其他**元件）。  
  
## <a name="see-also"></a>另請參閱  
 [關於 SQL Server 授權條款](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  
