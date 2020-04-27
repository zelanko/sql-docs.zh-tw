---
title: 從命令提示字元安裝 Distributed Replay |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ea1171da-f50e-4f16-bedc-5e468a46477f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 67d74db6faf9b40ad323ed2948c2c0a596a63016
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63149742"
---
# <a name="install-distributed-replay-from-the-command-prompt"></a>從命令提示字元處安裝 Distributed Replay
  在命令提示字元處安裝 Distributed Replay 的新執行個體，讓您可以指定安裝功能及應如何設定。 命令提示字元安裝支援安裝、修復、升級及解除 Distributed Replay 元件。 透過命令提示字元安裝時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援使用 /Q 參數進行完整無訊息模式。  
  
> [!NOTE]  
>  如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。  
  
## <a name="installation-parameters"></a>安裝參數  
 最上層功能清單包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和工具。 工具功能會安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，以及其他共用元件。 若要安裝 Distributed Replay 元件，請指定下列參數：  
  
|元件|參數|  
|---------------|---------------|  
|Distributed Replay Controller|**DREPLAY_CTLR**|  
|Distributed Replay Client|**DREPLAY_CLT**|  
|管理工具|**工具**|  
  
> [!IMPORTANT]  
>  安裝 Distributed Replay 之後，您必須在控制器電腦與用戶端電腦上建立防火牆規則，並為目標伺服器上的每個用戶端電腦授與權限。 如需詳細資訊，請參閱 [完成安裝後步驟](complete-the-post-installation-steps.md)。  
  
 您可以使用下表中的參數來開發安裝的命令列指令碼。  
  
|參數|描述|支援的值|  
|---------------|-----------------|----------------------|  
|/CTLRSVCACCOUNT<br /><br /> **選擇性**|Distributed Replay Controller 服務的服務帳戶。|檢查帳戶和密碼|  
|/CTLRSVCPASSWORD<br /><br /> **選擇性**|Distributed Replay Controller 服務帳戶的密碼。|檢查帳戶和密碼|  
|/CTLRSTARTUPTYPE<br /><br /> **選擇性**|Distributed Replay Controller 服務的啟動類型。|自動<br /><br /> 停用<br /><br /> 手動|  
|/CTLRUSERS<br /><br /> **選擇性**|指定哪些使用者擁有 Distributed Replay Controller 服務的權限。|使用者帳戶字串的集合，以 " " (空格) 作為分隔符號<br /><br /> **重要事項**：當您設定 Distributed Replay Controller 服務時，可以指定將用來執行 Distributed Replay Client 服務的一個或多個使用者帳戶。 下列是支援帳戶的清單：<br /><br /> 網域使用者帳戶<br /><br /> 使用者建立的本機使用者帳戶<br /><br /> 系統管理員<br /><br /> 虛擬帳戶和 MSA (受管理的服務帳戶)<br /><br /> 網路服務、本機系統和系統<br /><br /> <br /><br /> 不接受群組帳戶 (本機或網域) 和其他內建帳戶 (例如 Everyone)。|  
|/CLTSVCACCOUNT<br /><br /> **選擇性**|Distributed Replay Client 服務的服務帳戶。|檢查帳戶和密碼|  
|/CLTSVCPASSWORD<br /><br /> **選擇性**|Distributed Replay 用戶端服務帳戶的密碼。|檢查帳戶和密碼|  
|/CLTSTARTUPTYPE<br /><br /> **選擇性**|Distributed Replay Client 服務的啟動類型。|自動<br /><br /> 停用<br /><br /> 手動|  
|/CLTCTLRNAME<br /><br /> **選擇性**|用戶端與 Distributed Replay Controller 服務通訊的電腦名稱。||  
|/CLTWORKINGDIR<br /><br /> **選擇性**|Distributed Replay Client 服務的工作目錄。|有效路徑|  
|/CLTRESULTDIR<br /><br /> **選擇性**|Distributed Replay Client 服務的結果目錄。|有效路徑|  
  
### <a name="sample-syntax"></a>範例語法：  
 **安裝 Distributed Replay Controller 元件**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CTLR /IAcceptSQLServerLicenseTerms /CTLRUSERS="domain\user1" "domain\user2" /CTLRSVCACCOUNT="domain\svcuser" /CTLRSVCPASSWORD="password" /CTLRSTARTUPTYPE=Automatic  
```  
  
 **安裝 Distributed Replay Client 元件**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CLT /IAcceptSQLServerLicenseTerms /CLTSVCACCOUNT="domain\svcuser" /CLTSVCPASSWORD="password" /CLTSTARTUPTYPE=Automatic /CLTCTLRNAME=ControllerMachineName /CLTWORKINGDIR="C:\WorkingDir" /CLTRESULTDIR="C:\ResultDir  
```  
  
  
