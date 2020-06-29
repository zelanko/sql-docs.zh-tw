---
title: 使用來源助理新增來源 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5e850b7c-4b89-42ad-b0a6-d63ac7cc9568
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b58b10508765580e0cffe9bd62099f3e2d69863
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439725"
---
# <a name="add-a-source-using-source-assistant"></a>使用來源小幫手加入來源
  本主題提供使用來源小幫手加入新來源的步驟，也會列出可以在 [加入新來源]**** 對話方塊上使用的選項。當您將來源小幫手拖放至 SSIS 設計師，即會顯示此對話方塊。  
  
### <a name="to-use-source-assistant-to-add-a-source"></a>使用來源小幫手加入來源  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟要加入來源元件的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
2.  將 [**來源**小幫手] 元件從 [SSIS 工具箱] 拖曳至 **[資料流程]** 索引標籤。您應該會看到 [**加入新來源**] 對話方塊。 下一節提供可以在對話方塊中使用之選項的詳細資訊。  
  
3.  在 [類型]**** 清單中選取目的地的類型。  
  
4.  在 [**連接管理員**] 清單中選取現有的連線管理員，或選取 **\<New>** 以建立新的連線管理員。  
  
5.  如果您選取現有的連線管理員，請按一下 [確定]****，以關閉 [加入新目的地]**** 對話方塊。 您應該會看到目的地和連線管理員已加入資料流程。  
  
6.  如果您按一下 **\<New>** 以建立新的連線管理員，您應該會看到 [**連線管理員**] 對話方塊，可讓您指定連接的參數。 完成建立新的連接管理員之後，您會在 SSIS 設計師中看到目的地和連接管理員。  
  
  
