---
title: 執行封裝工作編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executepackagetask.parameter.F1
- sql12.dts.designer.executepackagetask.package.f1
- sql12.dts.designer.executepackagetask.general.f1
ms.assetid: c2c96b4f-eb10-4d8b-be34-88edfd0785fb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ff63c6568f0a34a43caf6765e7e01ce8022e10f0
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382256"
---
# <a name="execute-package-task-editor"></a>執行封裝工作編輯器
  使用「執行封裝工作編輯器」設定「執行封裝」工作。 「執行封裝」工作可讓封裝將其他封裝當做工作流程的一部分執行，以延伸 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的企業功能。  
  
 **您想要做什麼事？**  
  
-   [開啟 [執行封裝工作編輯器]](#open)  
  
-   [設定 [一般] 頁面上的 [選項]](#general)  
  
-   [設定 [封裝] 頁面上的 [選項]](#package)  
  
-   [設定 [參數繫結] 頁面上的 [選項]](#parameter)  
  
##  <a name="open"></a> 開啟 [執行封裝工作編輯器]  
  
1.  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中開啟包含 [執行封裝] 工作的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 專案。  
  
2.  以滑鼠右鍵按一下 SSIS 設計師中的工作，然後按一下 [編輯]。  
  
##  <a name="general"></a> 設定 [一般] 頁面上的 [選項]  
 **名稱**  
 為執行封裝工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入「執行封裝」工作的描述。  
  
##  <a name="package"></a> 設定 [封裝] 頁面上的 [選項]  
 **ReferenceType**  
 為專案中的子封裝選取 [專案參考]。 為封裝外部的子封裝選取 [外部參考]  
  
> [!NOTE]  
>  [ReferenceType] 選項是唯讀的，如果尚未將包含封裝的專案轉換為專案部署模型，則該選項設為 [外部參考]。 如需轉換的詳細資訊，請參閱 [將專案部署至 Integration Services 伺服器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
 **密碼**  
 如果子封裝受到密碼保護，請提供子封裝的密碼，或按一下省略符號 ([...]) 按鈕，然後建立子封裝的新密碼。  
  
 `ExecuteOutOfProcess`  
 指定子封裝是在父封裝的處理序中執行，還是在個別的處理序中執行。 根據預設，「 執行封裝 」 工作的 ExecuteOutOfProcess 屬性設為`False`，並執行相同的處理序與父封裝中的子封裝。 如果您將此屬性設定為 `true`，子封裝就會在不同的處理序中執行。 這可能會降低子封裝的啟動速度。 另外，如果此屬性設定為 `true`，則無法在僅限工具安裝中偵錯封裝；您必須安裝 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 產品。 如需詳細資訊，請參閱[安裝 Integration Services](install-windows/install-integration-services.md)。  
  
### <a name="referencetype-dynamic-options"></a>ReferenceType 動態選項  
  
#### <a name="referencetype--external-reference"></a>ReferenceType = 外部參考  
 **位置**  
 選取子封裝的位置。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**SQL Server**|設定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的位置。|  
|**檔案系統**|設定檔案系統的位置。|  
  
 **[連接]**  
 選取子封裝的儲存位置類型。  
  
 **PackageNameReadOnly**  
 顯示封裝名稱。  
  
#### <a name="referencetype--project-reference"></a>ReferenceType = 專案參考  
 **PackageNameFromProjectReference**  
 選取專案中包含的封裝，做為子封裝。  
  
### <a name="location-dynamic-options"></a>位置動態選項  
  
#### <a name="location--sql-server"></a>位置 = SQL Server  
 **[連接]**  
 在清單中選取 OLE DB 連線管理員，或按一下 [\<新增連線…>] 建立新的連線管理員。  
  
 **相關主題：**[OLE DB 連線管理員](connection-manager/ole-db-connection-manager.md)，[設定 OLE DB 連接管理員](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **PackageName**  
 輸入子封裝的名稱，或按一下省略符號 ([...])，然後找出該封裝。  
  
#### <a name="location--file-system"></a>位置 = 檔案系統  
 **[連接]**  
 在清單中選取檔案連線管理員，或按一下 [\<新增連線...>]，即可建立新的連線管理員。  
  
 **相關主題：**[檔案連線管理員](connection-manager/file-connection-manager.md)，[檔案連接管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **PackageNameReadOnly**  
 顯示封裝名稱。  
  
##  <a name="parameter"></a> 設定 [參數繫結] 頁面上的 [選項]  
 您可以將值從父封裝或專案傳遞至子封裝。 專案必須使用專案部署模型，而且子封裝必須包含在包含父封裝的相同專案中。  
  
 如需將專案轉換為專案部署模型的資訊，請參閱 [將專案部署至 Integration Services 伺服器](../../2014/integration-services/deploy-projects-to-integration-services-server.md)。  
  
 **子封裝參數**  
 輸入或選取子封裝參數的名稱。  
  
 **繫結參數或變數**  
 選取包含您要傳遞到子封裝之值的參數或變數。  
  
 **[加入]**  
 按一下此選項可將參數或變數對應到子封裝參數。  
  
 **移除**  
 按一下此選項可移除參數或變數與子封裝參數之間的對應。  
  
  
