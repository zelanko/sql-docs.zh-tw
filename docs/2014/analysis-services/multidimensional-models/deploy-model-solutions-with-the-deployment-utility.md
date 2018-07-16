---
title: 使用部署公用程式部署模型方案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- deploying [Analysis Services], command prompt
- command prompt utilities [SQL Server], Microsoft.AnalysisServices.Deployment
- Microsoft.AnalysisServices.Deployment utility
- Analysis Services deployments, command prompt
ms.assetid: 584f78ac-5f18-41e0-b292-d1949ec05196
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dd29d0d9c3a49712cdb14f219070f071a8575eae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330498"
---
# <a name="deploy-model-solutions-with-the-deployment-utility"></a>使用部署公用程式的部署模型方案
   **Microsoft.AnalysisServices.Deployment** 公用程式可讓您在命令提示字元之下啟動 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署引擎。 這個公用程式利用在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中建立 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]專案所產生的 XML 輸出檔來作為輸入檔。 您可以輕易地修改這些輸入檔來自訂 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的部署。 產生的部署指令碼可以立即執行，或儲存供稍後進行部署使用。  
  
## <a name="syntax"></a>語法  
  
```  
  
      Microsoft.AnalysisServices.Deployment [ASdatabasefile]   
    {[/s[:logfile]] | [/a] | [[/o[:output_script_file]] [/d]]}  
```  
  
##  <a name="Arguments"></a> 引數  
 *ASdatabasefile*  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署指令碼 (.asdatabase) 檔案所在之資料夾的完整路徑。 當您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中部署專案時，就會產生這個檔案。 它位於專案 bin 資料夾。 .asdatabase 檔案包含要部署之物件定義所在的位置。 如果未指定的話，則會使用目前的資料夾。  
  
 **/s**  
 以無訊息模式執行公用程式，不顯示任何對話方塊。 如需模式的詳細資訊，請參閱這個主題稍後的 [模式](#Modes)一節。  
  
 *logfile*  
 記錄檔的完整路徑和檔案名稱。 追蹤事件會記錄在指定的記錄檔中。 如果記錄檔已經存在，就會取代檔案的內容。  
  
 **/a**  
 以回應模式執行公用程式。 在公用程式精靈部分的作業期間所產生的所有回應都應該寫回輸入檔中，但不會在部署目標上進行任何實際的變更。  
  
 **/o**  
 以輸出模式執行公用程式。 不會進行部署，但通常傳給部署目標的 XML for Analysis (XMLA) 指令碼會儲存在指定的輸出指令碼檔案中。 如果未指定 *output_script_file* ，公用程式會嘗試使用部署選項 (.deploymentoptions) 輸入檔中指定的輸出指令碼檔案。 如果部署選項輸入檔並未指定輸出指令碼檔案，就會發生錯誤。  
  
 如需模式的詳細資訊，請參閱這個主題稍後的 [模式](#Modes)一節。  
  
 *output_script_file*  
 輸出指令碼檔案的完整路徑和檔案名稱。  
  
 **/d**  
 如果使用 **/o** 引數，則指定公用程式不應連接目標執行個體。 由於不會建立與部署目標的連接，因此，只會根據從輸入檔擷取的資訊來產生輸出指令碼。  
  
> [!NOTE]  
>  **/d** 引數只適用於輸出模式。 如果在回應或無訊息模式中指定這個引數，便會忽略它。 如需模式的詳細資訊，請參閱這個主題稍後的 [模式](#Modes)一節。  
  
## <a name="remarks"></a>備註  
 **Microsoft.AnalysisServices.Deployment** 公用程式會使用一組提供物件定義、部署目標、部署選項和組態設定的檔案，且會嘗試利用指定的部署選項和組態設定，將物件定義部署到指定的部署目標中。 當在回應檔或輸出模式中叫用這個公用程式時，它可以提供一個使用者介面。 如需如何利用提供給這個公用程式的使用者介面來建立回應檔的詳細資訊，請參閱 [使用部署精靈來部署模型方案](deploy-model-solutions-using-the-deployment-wizard.md)。  
  
 此公用程式位於 \Program files (x86)\Microsoft SQL Server\110\Binn\ManagementStudio 資料夾。  
  
##  <a name="Modes"></a> 模式  
 可以使用下表列出的模式來執行這個公用程式。  
  
|[模式]|描述|  
|----------|-----------------|  
|無訊息模式|不顯示任何使用者介面，部署所需要的所有資訊都由輸入檔提供。 在無訊息模式下，此公用程式不會顯示任何進度。 相反地，您可以利用選擇性的記錄檔來擷取進度和錯誤資訊，以便稍後進行檢閱。|  
|回應模式|這個模式會顯示部署精靈使用者介面，使用者回應會儲存在指定的輸入檔中，以便稍後進行部署。 回應模式下不會進行部署。 回應模式的唯一用途是擷取使用者回應。|  
|輸出模式|不顯示任何使用者介面，部署所需要的所有資訊都由輸入檔提供。<br /><br /> 不過，公用程式的輸出會寫入輸出指令碼檔案中，而不是傳給輸入檔所指出的部署目標，與無訊息模式不同。 除非指定了 **/d** 引數；否則，公用程式會在產生輸出指令碼檔案時，連接每個部署目標來比較中繼資料。|  
  
 [返回引數](#Arguments)  
  
## <a name="examples"></a>範例  
 下列範例會顯示如何在無訊息模式中部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，將進度和錯誤訊息記錄下來，以便稍後進行檢閱：  
  
 `Microsoft.AnalysisServices.Deployment.exe`  
  
 `<drive>:\My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin`  
  
 `/s: C:\ My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin\deployment.log`  
  
## <a name="see-also"></a>另請參閱  
 [命令提示字元公用程式參考 &#40;Database Engine&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
