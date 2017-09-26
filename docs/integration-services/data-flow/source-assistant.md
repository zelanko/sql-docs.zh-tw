---
title: "來源小幫手 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9b7406edf9f7234db739730473772d77c42399ec
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="source-assistant"></a>Source Assistant
  來源小幫手元件有助於建立來源元件和連線管理員。 該元件位於 SSIS 工具箱的 **[我的最愛]** 區段中。  
  
> [!NOTE]  
>  來源小幫手取代了 Integration Services 連接專案和對應的精靈。  
  
## <a name="add-a-source-with-source-assistant"></a>加入來源使用來源小幫手
本節提供步驟，加入新的來源，使用來源小幫手，並且也會列出可用的選項**加入新來源**對話方塊，您會看到當您拖曳來源小幫手至 SSIS 設計工具。  

1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟要加入來源元件的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  將 [來源小幫手] 元件從 SSIS 工具箱拖曳至 [資料流程] 索引標籤。[加入新來源] 對話方塊應會隨即出現。 下一節提供可以在對話方塊中使用之選項的詳細資訊。  
  
3.  在 [類型] 清單中選取目的地的類型。  
  
4.  選取現有的連接管理員中**連接管理員**清單或選取**\<新增 >**以建立新的連接管理員。  
  
5.  如果您選取現有的連線管理員，請按一下 [確定]，以關閉 [加入新目的地] 對話方塊。 您應該會看到目的地和連線管理員已加入資料流程。  
  
6.  如果您按一下**\<新增 >**若要建立新的連接管理員，您應該看到**連線管理員**對話方塊，可讓您指定連接參數。 完成建立新的連接管理員之後，您會在 SSIS 設計師中看到目的地和連接管理員。  

## <a name="add-new-source-dialog-box"></a>加入新來源對話方塊
下表列出可用選項中**加入新來源** 對話方塊。  
  
|選項|說明|  
|------------|-----------------|  
|類型|選取您要連接的來源類型。|  
|連接管理員|選取現有的連接管理員，或按一下**\<新增 >**以建立新的連接管理員。|  
|僅顯示已安裝|指定是否只要檢視已安裝的來源。|  
|確定|按一下以儲存您的變更，並開啟任何後續的對話方塊設定其他選項。| 
  
