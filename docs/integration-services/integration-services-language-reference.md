---
title: "Integration Services 語言參考 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
ms.assetid: c67b72f1-0a1e-42f0-878a-84e85efc915b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9fe4120f8a5dc93517e8eb35b13e7fe5252be6b6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-language-reference"></a>Integration Services 語言參考
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本節描述用來管理 [!INCLUDE[tsql](../includes/tsql-md.md)] 專案 (已部署至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的執行個體) 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] API。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會將物件、設定和作業資料儲存在名為 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目錄的資料庫中。 預設名稱[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]目錄是 SSISDB。 儲存在目錄中的物件包含了專案、封裝、參數、環境和作業歷程記錄。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目錄會將其資料儲存在不會對使用者顯示的內部資料表中。 不過，它會透過一組可供您查詢的公用檢視來公開您需要的資訊。 它也會提供一組預存程序，讓您可以用來在目錄上執行工作。  
  
 通常您會透過開啟 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 來管理目錄中的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 物件。 不過，您也可以直接使用資料庫檢視並呼叫預存程序，或編寫可呼叫 Managed API 的自訂程式碼。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 和 Managed API 會查詢檢視並呼叫本節中說明的預存程序，以執行許多工作。  
  
## <a name="in-this-section"></a>本節內容  
 [檢視 &#40; Integration Services 目錄 &#41;](../integration-services/system-views/views-integration-services-catalog.md)  
 查詢檢視，即可檢查 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件、設定和作業資料。  
  
 [預存程序 &#40; Integration Services 目錄 &#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
 呼叫預存程序，即可加入、移除或修改 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件和設定。  
  
 [函式 &#40;Integration Services 目錄&#41;](http://msdn.microsoft.com/library/9f2aec85-3d4c-415f-b1f8-8328a60b1c7f)  
 呼叫函數以管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
  

