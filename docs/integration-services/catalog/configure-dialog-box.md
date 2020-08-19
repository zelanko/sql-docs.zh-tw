---
description: 設定對話方塊
title: 設定對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.configure.f1
- sql13.SSIS.SSMS.ISPROJECTPROP.REFERENCES.F1
- sql13.SSIS.SSMS.ISPROJECTPROP.PARAMETERS.F1
ms.assetid: 10183c8d-b1be-420f-972a-96ea97d4f4d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cdbcc9b0a03b0afefe56152dc6b29c7ae59ea4cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395004"
---
# <a name="configure-dialog-box"></a>設定對話方塊

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  使用 **[設定]** 對話方塊來針對封裝和專案設定參數、連接管理員及環境的參考。  
  
 **您想要做什麼事？**  
  
-   [開啟設定對話方塊](#open_dialog)  
  
-   [在參數頁面上設定選項](#parameter)  
  
-   [在參考頁面上設定選項](#references)  
  
##  <a name="open-the-configure-dialog-box"></a><a name="open_dialog"></a> 開啟設定對話方塊  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
     您正在連線到裝載 SSISDB 資料庫的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。  
  
2.  在 [物件總管] 中，展開樹狀目錄以顯示 **[Integration Services 目錄]** 節點。  
  
3.  展開 **[SSISDB]** 節點。  
  
4.  展開包含您要設定之封裝或專案的資料夾。  
  
5.  以滑鼠右鍵按一下封裝或專案，然後按一下 [設定]****。  
  
##  <a name="set-the-options-on-the-parameters-page"></a><a name="parameter"></a> 在參數頁面上設定選項  
 使用 **[參數]** 頁面檢視參數名稱和值，並修改這些值。  
  
 選取 [參數]**** 和 [連線管理員]**** 索引標籤的 [範圍]**** 下拉式清單中所顯示之參數的範圍。  
  
 以下是 **[參數]** 索引標籤中的選項清單。  
  
 **容器**  
 列出包含參數的物件。  
  
 **名稱**  
 列出參數名稱。  
  
 **值**  
 列出參數值。 按一下省略符號按鈕，在 **[設定參數值]** 對話方塊中變更此值。  
  
 以下是 **[連接管理員]** 索引標籤中的選項清單。使用此索引標籤可變更連接管理員屬性的值。 SSIS 伺服器上會自動產生屬性的參數。  
  
 **容器**  
 列出包含連接管理員的物件。  
  
 **名稱**  
 列出連接管理員名稱。  
  
 **屬性名稱**  
 列出連接管理員屬性的名稱。  
  
 **值**  
 列出指派給連接管理員屬性的值。 按一下省略符號按鈕，在 **[設定參數值]** 對話方塊中變更此值。 您可以輸入常值、對應包含您要使用之值的環境變數，或使用封裝中的預設值。  
  
##  <a name="set-the-options-on-the-references-page"></a><a name="references"></a> 在參考頁面上設定選項  
 使用 **[參考]** 頁面加入及移除環境的參考，並存取環境屬性。  
  
 環境會針對已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器之專案中所包含的套件，指定執行值。  
  
 **環境**  
 列出環境。  
  
 **環境資料夾**  
 列出包含環境的資料夾。  
  
 **開啟**  
 按一下以開啟 [環境屬性]**** 對話方塊。  
  
 **加入**  
 按一下以加入環境的參考。 在 **[瀏覽環境]** 對話方塊中，按一下環境，然後按一下 **[確定]**。  
  
 您可以選取 **[SSISDB]** 節點底下的任何專案資料夾中所包含的環境。  
  
 **移除**  
 按一下 [參考]**** 區域中所列的環境，然後按一下 [移除]****。  
  
  
