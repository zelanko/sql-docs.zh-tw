---
title: "安全性屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- security [Analysis Services], properties
- SecurityPackageList property
- BuiltinAdminsAreServerAdmins property
- DisableClientImpersonation property
- ErrorMessageMode property
- RequiredProtectionLevel property
- ServiceAccountIsServerAdmin property
- RequireClientAuthentication property
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e99cf48fc3eb863b0a0d1e04fc19e83655ccc47f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="security-properties"></a>安全性屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的安全性伺服器屬性。 如需其他伺服器屬性以及如何設定伺服器屬性的詳細資訊，請參閱 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **適用於：** 多維度與表格式伺服器模式  
  
## <a name="properties"></a>屬性  
 **RequireClientAuthentication**  
 指出是否需要用戶端驗證的布林屬性。  
  
 此屬性的預設值為 True，表示用戶端驗證是必要的。  
  
 **SecurityPackageList**  
 此為字串屬性，包含 SSPI 封裝的逗號分隔清單，供伺服器的用戶端驗證使用。  
  
 **DisableClientImpersonation**  
 此為布林值屬性，指出用戶端模擬 (例如，從預存程序) 是否停用。  
  
 此屬性的預設值為 False，表示用戶端模擬是啟用的。  
  
 **BuiltinAdminsAreServerAdmins**  
 此為布林值屬性，指出本機電腦管理員群組的成員是否為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理員。  
  
 **ServiceAccountIsServerAdmin**  
 指出服務帳戶是否為伺服器管理員的布林屬性。  
  
 此屬性的預設值為 True，表示服務帳戶為伺服器管理員。  
  
 **ErrorMessageMode**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 **DataProtection\ RequiredProtectionLevel**  
 此為帶正負號的 32 位元整數屬性，其中定義所有必要的用戶端要求保護層級。 此屬性的值為下表列出的值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|*0*|無，允許純文字。|  
|*1*|(預設值) 需要有加密，不能以純文字記錄。|  
|*2*|允許純文字要求，但僅限於有簽章時 (保護弱於加密)。|  
  
 **AdministrativeDataProtection\ RequiredProtectionLevel**  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
