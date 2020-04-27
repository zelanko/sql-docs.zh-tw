---
title: 組建 Analysis Services 專案（SSDT） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], building
- Business Intelligence Development Studio, project building [Analysis Services]
ms.assetid: caac03cb-b2b4-4652-8913-3dd39c4b0127
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97e32b80d19675b3763101d1c226529a48e23e68
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66076777"
---
# <a name="build-analysis-services-projects-ssdt"></a>建立多個 Analysis Services 專案 (SSDT)
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的方式就像是在 Visual Studio 中建立任何程式設計專案。 當您建立此專案時，會在輸出目錄中建立一組 XML 檔案， 這些 XML 檔案會使用 Analysis Services 指令碼語言 (ASSL)，這種語言是用戶端應用程式 (包括 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ) 為了建立或修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件而與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體溝通所用的 XML 用語； 這些 XML 檔案是用來將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件定義部署到指定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
## <a name="building-a-project"></a>建立專案  
 當您建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 將會在輸出資料夾中建立一組完整的 XML 檔案，其中包括建立專案中所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫物件所需的所有必要 ASSL 命令。 如果之前已建立此專案，而且已針對使用中的組態指定累加部署，則 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 也將會建立包含 ASSL 命令的 XML 檔案，以便對已部署的物件執行累加更新； 此 XML 檔案會寫入到 ..\obj\\<使用中的組態\> 資料夾中。 當部署及處理極大的專案或資料庫時，累加建立的方式可以節省時間。  
  
> [!NOTE]  
>  您可以使用 [全部重建] 命令來忽略累加部署設定。  
  
 建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時，會驗證專案中的物件定義， 這項驗證包含任何參考的組件。 建立錯誤會出現在 [工作清單] 視窗中，連同分析管理物件 (AMO) 錯誤文字； 您可以按一下錯誤，開啟修正該錯誤所需的設計工具。  
  
 驗證成功並不保證在部署期間可以在目的地伺服器上建立物件，或是在部署之後可以處理成功。 下列問題可能會妨礙成功部署或部署之後的處理：  
  
-   未執行伺服器的安全性檢查，因此鎖定可能會妨礙部署。  
  
-   未在伺服器上驗證實體位置。  
  
-   未針對目的地伺服器上的實際資料來源檢查資料來源檢視的詳細資料。  
  
 如果驗證成功，則 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會產生 XML 檔案。 當組建之後，輸出資料夾中所包含的檔案如下表所示。  
  
|檔案 (在 bin 資料夾中)|描述|  
|-----------------------------|-----------------|  
|*Projectname*.asdatabase|包含 ASSL 元素，這些元素會在部署指令碼檔案中定義 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案內物件的中繼資料， 部署引擎會使用這個檔案將這些物件部署至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。|  
|*Projectname*.configsettings|包含部署期間可用來直接修改或在 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 中使用的組態設定 (例如，資料來源的連接字串)。|  
|*Projectname*.deploymenttargets|包含部署期間可用來直接修改或在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 「部署精靈」中使用的目的地設定 (例如，伺服器和資料庫名稱)。|  
|*Projectname*.deploymentoptions|包含部署期間可用來直接修改或在 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 中使用的各種選項設定 (例如，儲存位置)|  
|*Assemblyname*/*dllname。* urlmon.dll|每一個參考之組件的個別資料夾；每一個資料夾都包含該組件的 DLL、任何參考的組件，以及輸出偵錯資訊的所有關聯 .pdb 檔案。|  
  
|檔案 (在 obj 資料夾中)|描述|  
|-----------------------------|-----------------|  
|\<設定名稱> \LastBuilt.xml|包含時間戳記和雜湊碼，可用來識別上次建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的時間。|  
  
 這些 XML 檔案不包含\<Create> 和\<Alter> 標記，這是在部署期間所建立的。  
  
 參考的組件 (不包括標準系統和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 組件) 也會複製到輸出目錄中； 當參考方案中的其他專案時，會先使用適當的專案組態及這些專案參考所建立的組建相依性來建立這些專案，然後再複製到專案輸出資料夾中。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 &#40;ASSL&#41; 參考](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [部署 Analysis Services 專案 &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
