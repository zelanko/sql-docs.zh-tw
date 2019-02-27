---
title: SQL Server Analysis Services 伺服器管理 |Microsoft Docs
ms.date: 11/15/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 10623ea2c0dcb413bad08e1d68dfd9d5c9a9984a
ms.sourcegitcommit: c3b190f8f87a4c80bc9126bb244896197a6dc453
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852883"
---
# <a name="sql-server-analysis-services-server-management"></a>SQL Server Analysis Services 伺服器管理
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Azure Analysis services，請參閱[管理 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-manage)。

## <a name="instances"></a>執行個體

  Analysis Services 的伺服器執行個體是一份**msmdsrv.exe**當做作業系統服務執行的可執行檔。 每一個執行個體與相同伺服器上的其他執行個體之間完全獨立，而且擁有它自己的組態設定、權限、通訊埠、啟動帳戶、檔案儲存體和伺服器模式屬性。  
  
 Windows 服務 Msmdsrv.exe，在定義的登入帳戶的安全性內容中執行每個執行個體。  
  
-   預設執行個體的服務名稱是 MSSQLServerOLAPService。  
  
-   每個具名執行個體的服務名稱是 MSOLAP$ InstanceName。  
  
> [!NOTE]  
>  如果已安裝多個執行個體，安裝程式也會安裝重新導向程式服務，整合了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]瀏覽器服務。 重新導向程式服務會負責將用戶端導向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的適當具名執行個體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務一律會在本機服務帳戶的安全性內容中執行，本機服務帳戶是 Windows 針對不會存取本機電腦外部資源的服務所使用的受限使用者帳戶。  
  
 多重執行個體表示您可以在相同硬體上安裝多個伺服器執行個體來進行擴充。 尤其對於 Analysis Services 而言，這也表示您可以在相同伺服器上安裝多個執行個體 (每個執行個體都設定為在特定模式下執行) 來支援不同的伺服器模式。  

## <a name="server-mode"></a>伺服器模式
  
 伺服器模式是一種伺服器屬性，可決定用於該執行個體的儲存體和記憶體架構。 在多維度模式下執行的伺服器會使用針對多維度 Cube 資料庫和資料採礦模型所建立的資源管理層。 相較之下，表格式伺服器模式會使用 VertiPaq 記憶體中分析引擎和資料壓縮，在要求時彙總資料。  
  
 儲存體和記憶體架構之間的差異表示單一 Analysis Services 執行個體將會執行表格式資料庫或多維度資料庫，但不會兩者都執行。 伺服器模式屬性會決定哪一種類型的資料庫在執行個體上執行。  
  
 在安裝過程中，當您指定將在伺服器上執行的資料庫類型時，將會設定伺服器模式。 若要支援所有可用模式，您可以安裝多個 Analysis Services 執行個體，每個執行個體都使用與您建立之專案相對應的伺服器模式來部署。  
  
 通常，您必須執行的大部分管理工作不會因模式而改變。 您身為 Analysis Services 系統管理員，可以使用相同的程序和指令碼來管理網路上的任何 Analysis Services 執行個體，不論其安裝方式為何。  
  
> [!NOTE]  
>  例外狀況是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 部署的伺服器管理一定會在 SharePoint 伺服陣列的內容中進行。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 與其他伺服器模式不同之處在於它永遠都是單一執行個體，而且一定會透過 SharePoint 管理中心或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具來管理。 雖然可在 SQL Server Management Studio 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中連接到 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]for SharePoint，但是不需要這樣做。 SharePoint 伺服器陣列包含的基礎結構會同步處理伺服器狀態及監視伺服器可用性。 使用其他工具可能會干擾這些作業。 如需詳細資訊[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]伺服器的管理，請參閱 < [Powerpivot for SharePoint ](../../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)。  
  
  
  
## <a name="see-also"></a>另請參閱  
 [比較表格式和多維度解決方案 ](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
