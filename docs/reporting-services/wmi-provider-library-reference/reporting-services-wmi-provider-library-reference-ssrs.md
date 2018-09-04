---
title: Reporting Services WMI 提供者程式庫參考 (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: wmi-provider-library-reference
ms.suite: pro-bi
ms.topic: conceptual
apiname:
- Reporting Services WMI Provider Library
apilocation:
- reportingservices.mof
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ad028730c329857cc7072e6bda11966edfa9ba97
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43272718"
---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Reporting Services WMI 提供者程式庫參考 (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows Management Instrumentation (WMI) 提供者支援 WMI 作業，可讓您寫入指令碼和程式碼，以便修改報表伺服器和報表管理員的設定。  
  
 例如，如果您想要變更報表伺服器連接至報表伺服器資料庫時是否使用整合式安全性的設定，請建立 MSReportServer_ConfigurationSetting 類別的執行個體，然後使用報表伺服器執行個體的 DatabaseIntegratedSecurity 屬性。 下表所列出的類別代表 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件。 這些類別定義於 [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] 或 [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] 命名空間中。 其中每個類別都支援讀取和寫入作業。 但是，不支援建立作業。  
  
## <a name="classes"></a>類別  
 [MSReportServer_Instance 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-class.md)  
 提供用戶端連接至已安裝之報表伺服器所需的基本資訊。  
  
 [MSReportServer_ConfigurationSetting 類別](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
 代表報表伺服器執行個體的安裝與執行階段參數。 這些參數是儲存在報表伺服器的組態檔中。  
  
 如需有關 WMI 作業的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 隨附的 WMI SDK 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [存取 Reporting Services WMI 提供者](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)   
 [技術參考 &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
