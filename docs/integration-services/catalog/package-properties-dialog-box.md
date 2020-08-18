---
description: 封裝屬性對話方塊
title: 套件屬性對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageprop.general.f1
- sql13.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2294c3b934aaef7691849b34f53cc6f4dc76d28d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88351524"
---
# <a name="package-properties-dialog-box"></a>封裝屬性對話方塊

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  使用 [封裝屬性]**** 對話方塊，檢視儲存在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器上之封裝的屬性。  
  
 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 伺服器](../integration-services-ssis-packages.md)。  
  
 **您想要做什麼事？**  
  
-   [開啟 [封裝屬性] 對話方塊](#open_dialog)  
  
-   [設定選項](#options)  
  
##  <a name="open-the-package-properties-dialog-box"></a><a name="open_dialog"></a> 開啟 [封裝屬性] 對話方塊  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
     您正在連線到裝載 SSISDB 資料庫的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。  
  
2.  在 [物件總管] 中，展開樹狀目錄以顯示 **[Integration Services 目錄]** 節點。  
  
3.  展開 **[SSISDB]** 節點。  
  
4.  展開包含您要檢視其屬性之封裝的資料夾。  
  
5.  以滑鼠右鍵按一下封裝，然後選取 [屬性]****。  
  
##  <a name="configure-the-options"></a><a name="options"></a> 設定選項  
 使用 [一般]**** 頁面，即可檢視所選封裝的屬性。  
  
 [一般]**** 頁面上的所有屬性都是唯讀的。  
  
 **名稱**  
 顯示封裝名稱。  
  
 **識別碼**  
 列出封裝識別碼。  
  
 **進入點**  
 [True]**** 值表示封裝是直接啟動。 [False]**** 值表示封裝是使用「執行封裝」工作，由另一個封裝啟動。 預設值是 **True**。  
  
 以滑鼠右鍵按一下方案總管中的封裝，然後按一下 [進入點封裝]****，就可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中為父封裝和子封裝設定此屬性。  
  
 **說明**  
 顯示封裝的選擇性描述。  
  
  
