---
title: 安全開發 (Reporting Services) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- development security [Reporting Services]
- security [Reporting Services], development
- security [Reporting Services], strategies
ms.assetid: 12161a6c-b93b-4312-9d27-0c922561eb9b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7ead476f8aa6d2565c1865a24c2570a68c2b958d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "63193809"
---
# <a name="secure-development-reporting-services"></a>安全開發 (Reporting Services)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 提供了強固的安全性系統，可在嚴格控制、管理員定義的安全性環境中執行程式碼。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 安全性系統，也稱為程式碼存取安全性 (或是證據型安全性)。 在程式碼存取安全性之下，系統會信任使用者存取資源，但是如果使用者執行的程式碼未獲得信任，該資源的存取將會遭到拒絕。  
  
 根據程式碼的安全性 (相對於特定使用者) 可允許針對 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 開發的自訂組件或資料、傳遞、轉譯和安全性延伸模組來表示安全性。 您的延伸模組程式碼可由任意數目的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 使用者來執行，這些使用者在開發時間都是未知的。 您所開發的自訂組件或延伸模組需要 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的特定安全性原則。 這些安全性原則會表示為 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中的類型。 如需有關程式碼存取安全性的詳細資訊，請參閱 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 文件集中的「程式碼存取安全性」。  
  
## <a name="in-this-section"></a>本節內容  
 [Reporting Services 中的程式碼存取安全性](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)  
 介紹 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中自訂組件和延伸模組的程式碼存取安全性和原則組態。  
  
 [了解安全性原則](../../../reporting-services/extensions/secure-development/understanding-security-policies.md)  
 描述 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的各種組件類型，以及程式碼存取安全性如何影響程式碼權限。  
  
 [使用 Reporting Services 安全性原則檔](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)  
 描述不同的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 元件及對應的原則組態檔。  
  
  
