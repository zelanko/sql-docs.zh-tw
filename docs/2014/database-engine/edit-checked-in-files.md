---
title: 編輯簽入的檔案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying checked-in files
- checking in files
ms.assetid: 560cd19f-ab22-4273-b00c-149993a630e6
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: e2dbe1aad203dfdc83e438d5b7f4ed19c15038c1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933109"
---
# <a name="edit-checked-in-files"></a>編輯簽入的檔案
  您通常必須先簽出原始檔控制檔案，才能編輯它們。 不過，您可以設定， [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 讓您可以修改尚未簽出的檔案。這麼做時，您的變更會保留在記憶體中，直到您儲存檔案為止。 之後，系統會提示您從原始檔控制中簽出檔案。  
  
 如果您在進行團隊工作，除非您的原始檔控制提供者支援簽出本機版本，也支援簽出伺服器版本，否則，不建議您允許編輯簽入的檔案。 大部份提供者都不支援本機版本簽出項目。 如果您的提供者不支援簽出本機版本，且您編輯簽入的檔案，您就必須先手動合併在記憶體中的版本和伺服器版本，之後，才能簽入檔案。 在這個情況下，不支援自動合併及提供者輔助的合併。  
  
### <a name="to-edit-checked-in-files"></a>編輯簽入的檔案  
  
1.  在 **[工具]** 功能表上，按一下 **[選項]** 。  
  
2.  在 [**選項**] 對話方塊中，展開 [ **Source 控制**l] 資料夾，然後按一下 [**環境**]。  
  
3.  按一下 [**允許編輯簽入的專案**]，然後按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [管理簽入](../../2014/database-engine/manage-checkins.md)   
 [管理簽出](../../2014/database-engine/manage-checkouts.md)  
  
  
