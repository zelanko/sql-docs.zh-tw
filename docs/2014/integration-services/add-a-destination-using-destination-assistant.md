---
title: 使用目的地輔助程式新增目的地 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 747a0de0-3c2f-4d31-a692-7111fc0911d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd36828a7bab7fb33b86765f9f064b6406a17a9a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439755"
---
# <a name="add-a-destination-using-destination-assistant"></a>使用目的地小幫手來加入目的地
  本主題提供使用目的地小幫手來加入新目的地的步驟，也會列出可在 [加入新目的地]**** 對話方塊上使用的選項。當您將目的地小幫手拖放至 SSIS 設計師時，即會顯示此對話方塊。  
  
### <a name="to-use-destination-assistant-to-add-a-destination"></a>使用目的地小幫手加入目的地  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟要加入目的地元件的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
2.  將 [**目的地助理**] 元件從 [SSIS 工具箱] 拖曳至 **[資料流程]** 索引標籤。您應該會看到 [**加入新目的地**] 對話方塊。 下一節提供可以在對話方塊中使用之選項的詳細資訊。  
  
3.  在 [類型]**** 清單中選取目的地的類型。  
  
4.  在 [**連接管理員**] 清單中選取現有的連線管理員，或選取 **\<New>** 以建立新的連線管理員。  
  
5.  如果您選取現有的連線管理員，請按一下 [確定]****，以關閉 [加入新目的地]**** 對話方塊。 您應該會看到目的地和連線管理員已加入資料流程。  
  
6.  如果您按一下 **\<New>** 以建立新的連線管理員，您應該會看到 [**連線管理員**] 對話方塊，可讓您指定連接的參數。 完成建立新的連接管理員之後，您會在 SSIS 設計師中看到目的地和連接管理員。  
  
  
