---
title: 將腳本遷移至 VSTA |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSIS Script task, converting scripts
- Script component [Integration Services], converting scripts
- Script task [Integration Services], converting scripts
- SSIS Script component, converting scripts
ms.assetid: d685098b-86a1-46bf-939a-63d56951e009
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cb44a7b635e24c0c2e3266c1cca98a9c4f6a347c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093990"
---
# <a name="migrate-scripts-to-vsta"></a>將指令碼移轉到 VSTA
  當您將[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]封裝升級[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]為[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]時，會將任何腳本工作或腳本元件中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]的腳本遷移至 Tools for Applications （VSTA）。 VSTA 是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所使用的指令碼環境。 在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中，的腳本環境[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]是[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] for Applications （VSA）。  
  
 如果指令碼工作或指令碼元件中的指令碼會參考介面，您可能必須在升級封裝以前修改這些參考。 否則，此封裝將無法升級或指令碼將無法驗證 (視您所使用的升級方法而定)。 若要修改這些參考，請以對應的 IDTS*xxx*100 介面的參考取代 IDTS*xxx*90 介面的參考。  
  
 如需如何遷移腳本和升級封裝的詳細資訊，請參閱[升級 Integration Services 套件](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
## <a name="understanding-migration-failures"></a>了解移轉失敗  
 當您移轉指令碼時，移轉可能會因為下列其中一個原因而失敗：  
  
-   VSA 指令碼的進入點已重新命名。  
  
     進入點將 VSTA 專案中 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段所呼叫的 `ScriptMain` 類別方法指定為指令碼工作程式碼的進入點。 `ScriptMain` 類別是指令碼範本所產生的預設類別。  
  
-   VSA 指令碼中沒有任何進入點，或者含有多個進入點。  
  
-   無法加入組件參考。  
  
-   `ScriptMain` 類別已修改為除了 `ScriptObjectModelSSIS` 類別之外，也會繼承其他類別。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]不支援多重繼承。  
  
 您無法將使用[!INCLUDE[vbprvblong](../../includes/vbprvblong-md.md)]的 VSA 腳本轉換成使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]的 VSTA 腳本。 不過，您可以建立使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)]的新 VSTA 腳本。 如需詳細資訊，請參閱[指令碼工作的程式碼撰寫和偵錯](../../integration-services/control-flow/script-task.md)和[指令碼元件的程式碼撰寫和偵錯](../../integration-services/data-flow/transformations/script-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用指令碼擴充套件](../../relational-databases/server-management-objects-smo/tasks/scripting.md)  
  
  
