---
title: "開啟範本 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-templates
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [Transact-SQL], opening
- opening templates
ms.assetid: 605b0f4c-5ba1-4249-ad1c-6341df77cd7a
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3a847e96967fc4c9a07fdd0afdc2247bded22fd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="open-a-template"></a>開啟範本
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 您可以從範本總管開啟範本。  
  
## <a name="to-open-a-template-from-template-explorer"></a>若要從範本總管開啟範本  
您可以從範本總管開啟範本。  
  
1.  若要開啟範本總管，請按一下 [檢視] 功能表中的 [範本總管]。  
  
2.  在範本類別目錄清單中，展開包含要開啟之範本的類別目錄。  
  
3.  有三種方法可以開啟範本：  
  
    1.  按兩下範本，在程式碼編輯器視窗中開啟。  
  
    2.  在範本上按一下滑鼠右鍵，然後選取 [開啟]，以在程式碼編輯器視窗中開啟該範本。  
  
    3.  將範本拖曳到程式碼編輯器視窗，即可將範本程式碼加入至編輯器視窗的內容。  
  
開啟範本後，請使用 [取代範本參數] 對話方塊，將範本參數置換成您的值。  
  
如果開啟範本會啟動新的編輯器視窗，則開啟此視窗時，將會包含目前使用中連接的認證。 例如，如果當您開啟 CREATE DATABASE 範本時，您將焦點放在物件總管中的 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 執行個體，將會使用該執行個體的連接開啟新的編輯器視窗。 如果沒有使用中連接， [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] 將會顯示登入對話方塊。  
  
## <a name="see-also"></a>另請參閱  
[範本總管](../../ssms/template/template-explorer.md)  
[取代範本參數](../../ssms/template/replace-template-parameters.md)  
  
