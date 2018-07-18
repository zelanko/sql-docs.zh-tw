---
title: 套件屬性對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageprop.general.f1
- sql12.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a85a05d5a0b18701ed9b8a480ef0bb7c05e873d4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304208"
---
# <a name="package-properties-dialog-box"></a>封裝屬性對話方塊
  使用 [封裝屬性] 對話方塊，檢視儲存在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上之封裝的屬性。  
  
 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 伺服器](integration-services-ssis-server-and-catalog.md)。  
  
 **您想要做什麼事？**  
  
-   [開啟 [封裝屬性] 對話方塊](#open_dialog)  
  
-   [設定選項](#options)  
  
##  <a name="open_dialog"></a> 開啟 [封裝屬性] 對話方塊  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
     您正在連接到主控 SSISDB 資料庫之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體。  
  
2.  在 [物件總管] 中，展開樹狀目錄以顯示 **[Integration Services 目錄]** 節點。  
  
3.  展開 **[SSISDB]** 節點。  
  
4.  展開包含您要檢視其屬性之封裝的資料夾。  
  
5.  以滑鼠右鍵按一下封裝，然後選取 [屬性]。  
  
##  <a name="options"></a> 設定選項  
 使用 [一般] 頁面，即可檢視所選封裝的屬性。  
  
 [一般] 頁面上的所有屬性都是唯讀的。  
  
 **名稱**  
 顯示封裝名稱。  
  
 **識別碼**  
 列出封裝識別碼。  
  
 **進入點**  
 值`True`表示封裝直接啟動。 值`False`表示封裝由使用 「 執行封裝 」 工作的另一個封裝啟動。 預設值是 `True`。  
  
 以滑鼠右鍵按一下方案總管中的封裝，然後按一下 [進入點封裝]，就可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中為父封裝和子封裝設定此屬性。  
  
 **說明**  
 顯示封裝的選擇性描述。  
  
  
