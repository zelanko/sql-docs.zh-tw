---
title: 多重執行個體報表伺服器部署的 URL 保留項目 | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: f67c83c0-1f74-42bb-bfc1-e50c38152d3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a09d7c391af0d8800f5d9c66d40ab7ba0c2cbf4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "62513280"
---
# <a name="url-reservations-for-multi-instance-report-server-deployments"></a>多重執行個體報表伺服器部署的 URL 保留項目
  如果您在相同電腦上安裝多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體，您就必須考慮要如何為每一個執行個體定義 URL 保留項目。 在每一個執行個體中，報表伺服器 Web 服務和 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 至少每一個都必須有一個 URL 保留項目。 完整的保留項目集合在 HTTP.SYS 中必須是唯一的。  
  
 在 URL 註冊期間偵測到重複的 URL，這是在此服務啟動時發生。 如果您建立非唯一的 URL 保留項目，則要等到您啟動此服務之後，才可偵測到名稱衝突。 因此，請務必遵循命名慣例或規則，以確保所有的值都是唯一的。  
  
## <a name="default-naming-conventions"></a>預設命名慣例  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可安裝在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具名執行個體內。 當您在具名執行個體內安裝或設定報表伺服器時，執行個體名稱會自動包含在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供之預設 URL 保留項目的虛擬目錄中。 下表將顯示預設執行個體和具名執行個體的 URL 保留項目。  
  
|SQL Server 執行個體|預設 URL 保留項目|  
|-------------------------|-----------------------------|  
|預設值 (MSSQLServer)|`https://+:80/reportserver`|  
|已命名 (MynamedInstance)|`https://+:80/reportserver_MyNamedInstance`|  
  
 如果是具名執行個體，虛擬目錄會包含此執行個體名稱。 預設執行個體和具名執行個體都會接聽相同的通訊埠，但是唯一的虛擬目錄名稱會決定哪一個報表伺服器取得要求。  
  
 最佳做法建議是使用虛擬目錄名稱來區分報表伺服器執行個體， 這樣會清楚對應 URL 與目標執行個體，並確定應用程式名稱在整個系統中都是唯一的。  
  
## <a name="custom-naming-conventions"></a>自訂命名慣例  
 雖然建議使用執行個體名稱，但是您可以使用 URL 語法和自己的命名慣例，以符合 URL 保留項目的唯一名稱條件約束。 下列範例說明為每一個執行個體建立唯一 URL 的不同方式。  
  
|報表伺服器預設執行個體 (MSSQLSERVER)|ReportServer_MyNamedInstance|唯一性|  
|----------------------------------------------------|-----------------------------------|----------------|  
|`https://+:80/reportserver`|`https://+:8888/reportserver`|每個執行個體會接聽不同的通訊埠。|  
|`https://www.contoso.com/reportserver`|`https://SRVR-46/reportserver`|每一個執行個體都會對應到不同的伺服器名稱 (完整網域名稱和電腦名稱)。|  
  
## <a name="uniqueness-requirements"></a>唯一性規定  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用的基礎技術對於唯一的名稱有一些規定。 HTTP.SYS 要求它的儲存機制內的所有 URL 都必須是唯一的。 您可以讓通訊埠、主機名稱或虛擬目錄名稱不同，以建立唯一的 URL。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 要求相同處理序內的應用程式識別必須是唯一的。 這項規定會影響虛擬目錄名稱， 它指定您不能在相同的報表伺服器執行個體內重複虛擬目錄名稱。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
