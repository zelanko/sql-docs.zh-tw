---
title: Integration Services 程式設計概觀 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services, programming
- architecture [Integration Services]
- assemblies [Integration Services]
- SSIS, programming
- SQL Server Integration Services, programming
- run-time engine [Integration Services]
- packages [Integration Services], programming
- data flow engine [Integration Services]
- languages [Integration Services]
ms.assetid: 262babc6-eea5-4609-bc65-07d64cbcfee9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f540278d8f27eb091d4818f838d069c82a61159c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296218"
---
# <a name="integration-services-programming-overview"></a>Integration Services 程式設計概觀

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的架構會區隔資料移動和轉換與套件控制流程和管理。 定義這個架構的是兩個不同的引擎，當您針對 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 進行程式設計時，可以將這兩個引擎自動化及擴充。 執行階段引擎會實作控制流程和封裝管理基礎結構，該基礎結構可讓開發人員控制執行流程及設定記錄、事件處理常式和變數的選項。 資料流程引擎是一種特殊且高效率的引擎，它是專門用來擷取、轉換及載入資料。 在針對 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 進行程式設計時，您將會針對這兩個引擎進行程式設計。  
  
 下列影像說明 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的架構。  
  
 ![Integration Services 架構](../integration-services/media/mw-dts-01.gif "Integration Services 架構")  
  
## <a name="integration-services-run-time-engine"></a>Integration Services 執行階段引擎  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 執行階段引擎會控制封裝的管理與執行，其方式是實作可啟用執行順序、記錄、變數和事件處理的基礎結構。 針對 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 執行階段引擎進行程式設計，可讓開發人員將封裝的建立、組態設定和執行自動化，並建立自訂工作和其他延伸模組。  
  
 如需詳細資訊，請參閱[以指令碼工作擴充套件](../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)、[開發自訂工作](../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)和[以程式設計方式建置套件](../integration-services/building-packages-programmatically/building-packages-programmatically.md)。  
  
## <a name="integration-services-data-flow-engine"></a>Integration Services 資料流程引擎  
 資料流程引擎會管理資料流程工作，該工作是一項特殊且高效能的工作，專門用來移動及轉換各種不同來源中的資料。 與其他工作不同的是，資料流程工作包含了其他稱為資料流程元件的物件，這些可能是來源、轉換或目的地。 這些元件是此工作的核心移動部分， 它們會定義資料的移動和轉換。 針對資料流程引擎進行程式設計可讓開發人員將資料流程工作中元件的建立和組態設定自動化，並建立自訂元件。  
  
 如需詳細資訊，請參閱[以指令碼元件擴充資料流程](../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)、[開發自訂資料流程元件](../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)和[以程式設計方式建置套件](../integration-services/building-packages-programmatically/building-packages-programmatically.md)。  
  
## <a name="supported-languages"></a>支援的語言  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 完全支援 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]。 如此可讓開發人員使用所選的 .NET 相容語言來針對 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 進行程式設計。 雖然執行階段引擎和資料流程引擎都是以機器碼所撰寫，但是兩者都可透過完全受管理的物件模型來使用。  
  
 您可以在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)] 或是其他程式碼或文字編輯器中設計 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 套件、自訂工作和元件的程式。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 提供開發人員許多工具與功能，使之可以簡化及加快反覆執行程式碼撰寫、偵錯與測試週期的速度。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 也可簡化部署工作。 但是，您不需要 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 編譯及建立 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 程式碼專案。 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK 包含 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 和 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 編譯器與相關工具。  
  
> [!IMPORTANT]  
>  依預設，[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 會隨 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 一起安裝，但是不會安裝 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK。 除非已在電腦上安裝 SDK，而且 SDK 文件集是包含在線上叢書集合中，否則本節中的 SDK 內容連結將不會有任何作用。 在安裝 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK 之後，您可以遵循[新增或移除 SQL Server 的產品文件集](https://msdn.microsoft.com/library/ef798cc8-87cf-4d60-a7bf-9e061bdd0052)中的指示，將 SDK 文件集新增至線上叢書集合和目錄。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 指令碼工作和指令碼元件會將 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA) 作為內嵌指令碼環境使用。 VSTA 支援 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic 和 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 應用程式開發介面與 COM 指令碼語言 (如 VBScript) 不相容。  
  
## <a name="locating-assemblies"></a>尋找組件  
 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]中， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 組件已經升級至 .NET 4.0。 .NET 4 有個別的全域組件快取，位於 *磁碟機>\<* :\Windows\Microsoft.NET\assembly。 您可以在此路徑底下 (通常在 GAC_MSIL 資料夾中) 找到所有 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 組件。  
  
 如同舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，核心 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 擴充性 .dll 檔案也位於 *磁碟機>\<* :\Program Files\Microsoft SQL Server\100\SDK\Assemblies。  
  
## <a name="commonly-used-assemblies"></a>常用的組件  
 下表列出在使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 開發 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 程式時經常使用的組件。  
  
|組件|描述|  
|--------------|-----------------|  
|Microsoft.SqlServer.ManagedDTS.dll|包含 Managed 執行階段引擎。|  
|Microsoft.SqlServer.RuntimeWrapper.dll|包含原生執行階段引擎的主要 Interop 組件 (PIA) 或包裝函數。|  
|Microsoft.SqlServer.PipelineHost.dll|包含 Managed 資料流程引擎。|  
|Microsoft.SqlServer.PipelineWrapper.dll|包含原生資料流程引擎的主要 Interop 組件 (PIA) 或包裝函數。|  
  
  
