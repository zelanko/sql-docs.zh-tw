---
title: 維度處理目的地編輯器 （連線管理員頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.connection.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 44aab631-d62d-4895-8fc7-7f1f3b1b68ce
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1687baf77bcecedb61a3d1ecee3a9e3c9e155431
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133728"
---
# <a name="dimension-processing-destination-editor-connection-manager-page"></a>維度處理目的地編輯器 (連接管理員頁面)
  使用 **[維度處理目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面，來指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 計畫的連接或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]之執行個體的連接。  
  
 若要深入了解維度處理目的地，請參閱＜ [Dimension Processing Destination](data-flow/dimension-processing-destination.md)＞。  
  
## <a name="options"></a>選項。  
 **[ODBC 目的地編輯器]**  
 從清單中選取現有的連接管理員，或按一下 [新增] 來建立新的連接管理員。  
  
 **新增**  
 使用 [加入 Analysis Services 連接管理員] 對話方塊來建立新的連接。  
  
 **可用維度清單**  
 選取要處理的維度。  
  
 **處理方法**  
 選取要套用至清單中選取之維度的處理方法。 此選項的預設值是 **[完整]**。  
  
|值|描述|  
|-----------|-----------------|  
|**加入 (累加)**|執行維度的累加處理。|  
|**[完整]**|執行維度的完整處理。|  
|**Update**|執行維度的更新處理。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [維度處理目的地編輯器&#40;對應頁面&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)   
 [維度處理目的地編輯器&#40;進階頁面&#41;](../../2014/integration-services/dimension-processing-destination-editor-advanced-page.md)  
  
  
