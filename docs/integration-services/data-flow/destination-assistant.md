---
title: 目的地小幫手 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.destinationassistant.f1
- sql13.DTS.DESIGNER.DESTINATIONASSIST.F1
ms.assetid: 10a40921-a2c2-4ac8-be28-311f8500fbf6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5f302227746b0479f096fbfc29e50c328b61f114
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71292907"
---
# <a name="destination-assistant"></a>Destination Assistant

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  目的地小幫手元件有助於建立目的地元件和連線管理員。 該元件位於 SSIS 工具箱的 **[我的最愛]** 區段中。  
  
> [!NOTE]  
>  目的地小幫手取代了 Integration Services 連接專案和對應的精靈。  

## <a name="add-a-destination-with-destination-assistant"></a>使用目的地小幫手新增目的地
本主題提供使用目的地小幫手來加入新目的地的步驟，也會列出可在 [加入新目的地]  對話方塊上使用的選項。當您將目的地小幫手拖放至 SSIS 設計師時，即會顯示此對話方塊。  

1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟要加入目的地元件的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  將 [目的地小幫手]  元件從 SSIS 工具箱拖曳至 [資料流程]  索引標籤。[加入新目的地]  對話方塊應會隨即出現。 下一節提供可以在對話方塊中使用之選項的詳細資訊。  
  
3.  在 [類型]  清單中選取目的地的類型。  
  
4.  在 [連線管理員]  清單中選取現有的連線管理員，或選取 [\<新增>]  ，以建立新的連線管理員。  
  
5.  如果您選取現有的連線管理員，請按一下 [確定]  ，以關閉 [加入新目的地]  對話方塊。 您應該會看到目的地和連線管理員已加入資料流程。  
  
6.  如果按一下 [\<新增>]  來建立新的連線管理員，應會顯示 [連線管理員]  對話方塊，讓您指定連線參數。 完成建立新的連接管理員之後，您會在 SSIS 設計師中看到目的地和連接管理員。 
  
## <a name="add-new-destination-dialog-box"></a>新增新目的地對話方塊
下表列出可以在 [新增新目的地]  對話方塊中使用的選項。  
  
|選項|描述|  
|------------|-----------------|  
|類型|選取您要連接的目的地類型。|  
|連接管理員|選取現有的連線管理員，或按一下 [\<新增>]  以建立新的連線管理員。|  
|僅顯示已安裝|指定是否只要檢視已安裝的目的地。|  
|[確定]|按一下以儲存您的變更，並開啟任何後續的對話方塊設定其他選項。|  
