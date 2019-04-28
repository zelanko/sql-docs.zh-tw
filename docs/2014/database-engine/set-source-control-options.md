---
title: 設定原始檔控制選項 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Source_Control.Visual_SourceSafe
- VS.ToolsOptionsPages.Source_Control.General
- VS.ToolsOptionsPages.Source_Control.Environment
helpviewer_keywords:
- source controls [SQL Server Management Studio], options
ms.assetid: b2c6ca00-46f0-4f86-b067-07bae779c147
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0a654932689785d96aaff049551faf19494c311a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843711"
---
# <a name="set-source-control-options"></a>設定原始檔控制選項
  在利用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中所建立的原始檔控制功能之前，您應該先設定您的各種工作環境的原始檔控制選項。  
  
 您可以使用設定原始檔控制選項**選項**對話方塊來設定一或多個原始檔控制角色。 角色由您在其中使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 之設定的一般描述，以及這項設定的相關原始檔控制選項所組成。  
  
 例如，如果您是獨立的資料庫開發人員，則簽入檔案之後，通常會保留簽出的檔案，以避免與其他使用者發生衝突。 因此，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 會定義一個「獨立開發人員」角色。 針對此角色[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]會自動選取**保留項目簽出簽入時**選項。  
  
 由於您可以定義和自訂角色，因此，您可以使用各種開發設定來工作，且不需要在每次切換不同設定時，全面重新設定原始檔控制。  
  
### <a name="to-set-source-control-options"></a>設定原始檔控制選項  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]**。  
  
2.  在**選項**對話方塊方塊中，展開**原始檔控制**，然後按一下**外掛程式選取範圍**頁面。  
  
     **目前的原始檔控制外掛程式**  
     從此清單中選取您要使用的原始檔控制。 原始檔控制產品用戶端必須安裝在此電腦上，才會顯示在清單中。 如果電腦上未安裝原始檔控制用戶端，則唯一可用的選項將是「無」。 如果您已經安裝了 Microsoft Source Safe，則會顯示下列外掛程式：  
  
    -   Microsoft Visual SourceSafe  
  
    -   Microsoft Visual SourceSafe (網際網路)  
  
3.  針對您要使用的每個原始檔控制角色設定登入認證。 只有安裝了原始檔控制外掛程式之後，才可以使用此頁面。  
  
     **角色描述**  
     選取這些角色的其中之一，會自動選取適當的原始檔控制選項。  
  
    |角色|描述|  
    |----------|-----------------|  
    |**Visual SourceSafe**|指定您想要使用最常使用的設定[!INCLUDE[msCoName](../includes/msconame-md.md)]Visual SourceSafe 使用者。|  
    |**獨立開發人員**|指定您是獨立工作者。|  
    |**Custom**|指定您已修改角色的設定。|  
  
     **執行背景狀態更新**  
     項目狀態變更時，會自動更新方案總管中的原始檔控制訊號圖示。 如果您在執行需要大量伺服器的作業時遭遇延遲，尤其是從原始檔控制開啟方案或專案時，清除此核取方塊就可以改善效能。  
  
     **登入識別碼**  
     指定用來登入原始檔控制提供者的使用者名稱。 如果支援您的原始檔控制提供者，此名稱將會自動填入**登入**對話方塊，即可連線到您的原始檔控制伺服器。 若要讓這個選項成為使用中，請使用原始檔控制提供者的管理員程式，來停用自動使用者登入，然後重新啟動 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
     **進階**  
     顯示將項目加入原始檔控制的其他選項。 這些選項會視原始檔控制提供者而不同。 這些選項的說明是由原始檔控制程式所提供。  
  
4.  選取 **環境**頁面。  
  
5.  在 **原始檔控制環境設定**方塊中，選取您想要設定原始檔控制選項。  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 會自動選取所選角色的預設原始檔控制選項。 如果您清除任何預設選項，**原始檔控制環境設定**方塊會顯示**自訂**選項以指出您已自訂原來選取的角色。  
  
     **原始檔控制環境設定**  
     指定您要使用的角色。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 會定義下列角色。  
  
    |角色|描述|  
    |----------|-----------------|  
    |**Visual SourceSafe**|指定您想要使用最常使用的設定[!INCLUDE[msCoName](../includes/msconame-md.md)]Visual SourceSafe 使用者。|  
    |**獨立開發人員**|指定您是獨立工作者。|  
    |**Custom**|指定您已修改角色的設定。|  
  
     選取這些角色的其中之一，會自動選取適當的原始檔控制選項。  
  
     **保留項目時簽入簽出**  
     指定當您簽入項目以更新原始檔控制存放區時，項目應保持簽出。 如果您想要變更此特定簽入的選項，按一下**選項**中的箭號**簽入** 對話方塊中，然後再清除**保留簽出**核取方塊。  
  
     **簽入的項目**  
     會顯示一份指定的選項如何[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]您嘗試編輯某個未簽出的項目時的行為。下表描述可用的選項。  
  
     **正在儲存**  
  
    |動作|描述|  
    |------------|-----------------|  
    |**提示簽出**|顯示**簽出** 對話方塊。|  
    |**自動簽出**|簽出項目中，而不會顯示**簽出** 對話方塊。 這是預設選項。|  
    |**將儲存為**|另存為新的檔案。|  
  
     **編輯**  
  
    |動作|描述|  
    |------------|-----------------|  
    |**提示簽出**|顯示**簽出** 對話方塊。|  
    |**提示獨佔簽出**|顯示**簽出** 對話方塊。|  
    |**自動簽出**|簽出項目中，而不會顯示**簽出** 對話方塊。 這是預設選項。|  
    |**不執行任何動作**|不要將檔案簽出。|  
  
     **允許簽入的項目進行編輯**  
     指定已簽入的項目可以在記憶體中編輯。 如果您選取此核取方塊中，**編輯** 按鈕會出現在**簽出**對話方塊中，當您嘗試編輯已簽入項目。 按一下此按鈕之後，即可編輯項目。 如果您嘗試儲存項目，就必須將項目簽出或儲存到其他位置。  
  
     **重設**  
     將原始檔控制確認對話方塊重設為預設值。 例如，如果您已選取**不要再顯示此對話方塊**核取方塊，在 [原始檔控制] 對話方塊中，選取**重設**選項可以反轉該項動作。  
  
## <a name="see-also"></a>另請參閱  
 [原始檔控制基本概念](../../2014/database-engine/source-control-basics.md)   
 [變更原始檔控制連接](../../2014/database-engine/change-source-control-connections.md)   
 [從原始檔控制中排除檔案](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
