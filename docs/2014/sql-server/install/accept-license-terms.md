---
title: 接受授權合約 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 55d500b13cc3ab3c859474bb3050e29a7487f4a3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146430"
---
# <a name="accept-license-terms"></a>接受授權條款
  請使用 **安裝精靈的** [接受授權條款] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面來接受此版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的授權條款。  
  
 您可以列印授權合約，或將它複製到剪貼簿。 若要繼續，請接受授權條款，然後按 **[下一步]**。 若要結束安裝，請按一下 **[取消]**。  
  
## <a name="customer-experience-improvement-program-ceip"></a>客戶經驗改進計劃 (CEIP)  
 如果您啟用 CEIP 報表，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會設定為定期傳送報表至 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。 報表包含硬體組態及您如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和元件的相關資訊。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 將會使用功能使用方式資料來改進 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這項功能所監視的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件包括：  
  
-   的 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   複寫  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式  
  
 關於功能使用方式的資訊會傳送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] (以限制存取的方式予以儲存)。  
  
 若要在安裝程式完成之後停用 CEIP 報表，請使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態工具] 功能表中的 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤和使用方式報表] 工具。  
  
 對於安裝、升級、修復等等的安裝程式動作，僅會在執行安裝程式期間，收集並上傳資訊。  
  
 對於其他所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件，則會每天針對所有啟用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，收集一次資訊。 根據預設，收集的時間為午夜，好讓伺服器的負載減至最小。 如果您想要變更收集的時間，可手動編輯控制收集時間的登錄機碼。 每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體都擁有自己的登錄機碼：  
  
 HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\。\<執行個體識別碼 > \CPE\TimeofReporting  
  
 這個登錄機碼的值包含從 00:00 (午夜) 開始執行之收集時間的分鐘數。 例如，60 這個值會在 1:00 a.m. 執行收集，1200 這個值會在 8:00 p.m. 執行收集，以此類推。  
  
## <a name="error-reporting"></a>錯誤報告  
 使用 **安裝精靈的** [錯誤和使用方式報表設定] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面，可啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的功能錯誤和使用方式報告功能。  
  
### <a name="options"></a>選項。  
 根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 及其元件會停用功能使用方式資料收集和錯誤報告功能。  
  
 錯誤報告  
 如果您啟用錯誤報告功能，萬一下列任何一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件發生嚴重錯誤時，[!INCLUDE[msCoName](../../includes/msconame-md.md)] 就會設定為自動將報表傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   的 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   複寫  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 使用錯誤報表來改善[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]功能並將所有資訊視為機密。  
  
 關於錯誤的資訊會透過安全 (https) 連接傳送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] (以限制存取的方式予以儲存)。 另外，錯誤報表也可以傳送到您自己的 Corporate Error Reporting 伺服器。  
  
 錯誤報表包含下列資訊：  
  
-   發生問題時的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 狀況。  
  
-   作業系統版本和電腦硬體資訊。  
  
-   數位產品識別碼，它不是用於識別授權。  
  
-   電腦或 Proxy 伺服器的網路 IP 位址。  
  
-   導致錯誤之處理序的記憶體或檔案中的資訊。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不刻意收集檔案、 名稱、 地址、 電子郵件地址或其他形式的個人資訊。 不過，錯誤報表可包含導致錯誤之處理序的記憶體或檔案中的個人資訊。 雖然這項資訊可能用於判斷您的識別，但 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不會將這項資訊用於此用途。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 隱私權和資料收集原則的詳細資訊，請參閱 [Microsoft SQL Server 隱私權聲明](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md)。  
  
 如果您啟用錯誤報告卻發生嚴重錯誤，您可能會在 Windows 事件記錄檔中看到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的回應，它會指向關於特定錯誤的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知識庫文件。  
  
 在安裝程式完成之後，若要對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有執行個體及其元件停用錯誤或功能使用方式報表，請到 **[錯誤和使用方式報表設定]** 對話方塊，清除 **[功能使用方式]** 的核取方塊。 如果已對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的多個元件 ([!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和共用元件) 啟用 [錯誤報告]，您可以停用個別元件及共用元件 (以 [其他] 列出) 之每一個執行個體的錯誤報告。  
  
## <a name="see-also"></a>另請參閱  
 [關於 SQL Server 授權條款](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  