---
title: 報表伺服器狀態 （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serverstatus.F1
ms.assetid: 2f63ad1c-1bc2-449d-b451-fb39a0060838
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 52291c866e00100280c63253ef36b31bd8763948
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66428980"
---
# <a name="report-server-status-ssrs-native-mode"></a>報表伺服器狀態 (SSRS 原生模式)
  使用此頁面可檢視目前所連接之報表伺服器執行個體的相關資訊。 此頁面是報表伺服器組態的起始頁面。 其他頁面可用於設定 URL、服務帳戶、報表伺服器資料庫、報表伺服器電子郵件傳遞、向外延展部署和加密金鑰。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並連接到報表伺服器執行個體。 如需詳細資訊，請參閱 < [Reporting Services 組態管理員&#40;del&#41;](reporting-services-configuration-manager-native-mode.md)。  
  
> [!TIP]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]組態管理員 (RSConfigTool.exe) 使用"highestAvailable"權限層級安裝。 這是依據設計的行為。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員需要與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI API 進行通訊。 某些 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 通訊需要更高層級或系統管理權限。  
  
 如果您連接至報表伺服器，而且所有頁面連結都呈現灰色，請確認報表伺服器服務是否已啟動。 **報告服務狀態：** 應該是 「 已啟動 」。 您也可以使用 [系統管理工具] 中的 [服務] 主控台應用程式來檢查服務狀態。  
  
## <a name="options"></a>選項。  
 **SQL Server 執行個體**  
 顯示目前所連接報表伺服器執行個體的相關資訊。 報表伺服器執行個體名稱是以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具名執行個體為基礎。 預設執行個體為 MSSQLSERVER。 具名執行個體將會是您在安裝期間所指定的值。 如需有關執行個體的詳細資訊，請參閱[使用多個版本和 SQL Server 執行個體](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
> [!NOTE]  
>  在 SQL Server Express with Advanced Services 中，預設執行個體為 SQLExpress。  
  
 **執行個體識別碼**  
 對應至檔案系統上儲存您所連接之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的程式檔案的資料夾。 **[執行個體識別碼]** 值是由安裝程式使用 *&lt;component&gt;* . *&lt;instance&gt;* 格式指派的，其中 *&lt;component&gt;* 是表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的值，而 *&lt;instance&gt;* 是執行個體名稱。 預設執行個體名稱是 MSSQLSERVER。 例如，如果您安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件的預設執行個體，對應的資料夾名稱如下：  
  
-   MSSQL12.MSSQLSERVER  
  
-   MSAS12.MSSQLSERVER  
  
-   MSRS12.MSSQLSERVER  
  
 如果您安裝第二個元件的執行個體，您已安裝，這類[!INCLUDE[ssDE](../../includes/ssde-md.md)]，而且您將執行個體 Contoso**執行個體識別碼**是 MSSQL12。Contoso。  
  
 **版本(Edition)**  
 顯示版本資訊。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 版本支援的功能](https://go.microsoft.com/fwlink/?linkid=232473)。  
  
 **產品版本**  
 顯示您安裝的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本。  
  
 **報表伺服器資料庫**  
 顯示可儲存目前報表伺服器執行個體之應用程式資料的報表伺服器資料庫名稱。  
  
 **報表伺服器模式**  
 這裡顯示的值應該一律為 **[原生]** 。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員僅支援原生模式報表伺服器。 如果您看見 **SharePoint 整合模式**這個值，可能表示您的原生模式部署未正確設定，而且您需要連接到原生模式報表目錄。 使用組態管理員的 **[資料庫]** 頁面可變更資料庫，以及建立新的資料庫或連接到現有的原生模式報表伺服器資料庫目錄。  
  
 **伺服器狀態**  
 顯示報表伺服器服務是否在執行。  
  
 **啟動**  
 啟動報表伺服器服務。 在某些組態變更之後，就必須重新啟動此服務 (例如，在變更電腦名稱之後重新設定報表伺服器時)。 如果您重新設定 URL 保留項目，此服務將會自動重新啟動。 在挑選變更時，需要重新啟動。  
  
 **停止**  
 停止報表伺服器服務。 停止此服務會造成報表伺服器停止運作。 如需詳細資訊，請參閱 <<c0> [ 啟動和停止報表伺服器服務](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 F1 說明主題&#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Reporting Services 組態管理員&#40;del&#41;](/sql/sql-server/install/reporting-services-configuration-manager-native-mode)   
 [初始化報表伺服器 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
