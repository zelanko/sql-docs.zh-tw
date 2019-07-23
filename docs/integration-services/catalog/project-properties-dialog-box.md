---
title: 專案屬性對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isprojectprop.general.f1
- sql13.ssis.ssms.isprojectprop.permissions.f1
ms.assetid: d5cf52f5-1fe2-438a-98a3-fe117360acf8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f792df0fbfd7f78e82f0ce049dc1ef205576ae38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68007957"
---
# <a name="project-properties-dialog-box"></a>專案屬性對話方塊

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案是部署單位。 每個專案可以包含封裝、參數和環境參考。 專案為安全性物件，且可以定義資料庫主體的權限。 重新部署專案時，可以將舊版專案儲存到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄中。  
  
 專案參數和封裝參數可以用來在執行時間將值指派給封裝內的屬性。 有些參數會在封裝執行前要求值。 參考環境變數的參數值會要求專案在執行前已具有對應的環境參考。  
  
 **您想要做什麼事？**  
  
-   [開啟 [專案屬性] 對話方塊](#open_dialog)  
  
-   [設定 [一般] 頁面上的選項](#general)  
  
-   [設定 [權限] 頁面上的選項](#permissions)  
  
##  <a name="open_dialog"></a> 開啟 [專案屬性] 對話方塊  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
     您正在連線到裝載 SSISDB 資料庫的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。  
  
2.  在 [物件總管] 中，展開樹狀目錄以顯示 **[Integration Services 目錄]** 節點。  
  
3.  展開 **[SSISDB]** 節點。  
  
4.  展開包含您要設定其屬性之專案的資料夾。  
  
5.  以滑鼠右鍵按一下專案，然後再按一下 [屬性]  。  
  
##  <a name="general"></a> 設定 [一般] 頁面上的選項  
 使用 [一般] 頁面檢視專案屬性。  
  
 **名稱**  
 列出專案名稱。  
  
 **識別碼**  
 列出專案識別碼。  
  
 **說明**  
 顯示專案的選擇性描述。  
  
 **專案版本**  
 列出專案版本。  
  
 **部署日期**  
 列出部署或重新部署專案的日期和時間。  
  
##  <a name="permissions"></a> 設定 [權限] 頁面上的選項  
 使用 **[權限]** 頁面檢視並設定專案的明確權限。  
  
 瀏覽  
 按一下 [瀏覽]  ，使用 [瀏覽所有主體]  對話方塊選取您要設定其權限的使用者和角色。  
  
 **名稱**  
 列出使用者或角色的名稱。  
  
 **型別**  
 列出使用者或角色的類型。  
  
 **權限**  
 列出權限。  
  
 **授與者**  
 列出授與權限的使用者或角色。  
  
 **授與**  
 選取 [授與]  時，會針對使用者會或角色授與權限。  
  
 **拒絕**  
 選取 [拒絕]  時，會針對使用者會或角色拒絕權限。  
  
  
