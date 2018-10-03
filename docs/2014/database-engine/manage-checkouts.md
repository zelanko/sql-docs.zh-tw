---
title: 管理簽出 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], checkouts
- checkouts [SQL Server Management Studio]
- checking out files
ms.assetid: ddd4adba-d432-4005-9cb2-bb9ee3163d8e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9de9a1f8ceca0fbb05ab2b6680c5fcc34c951109
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183780"
---
# <a name="manage-checkouts"></a>管理簽出
  檔案加入原始檔控制之後，您必須先簽出檔案，才能修改它。 當您將檔案從原始檔控制中簽出時，原始檔控制提供者會在您的本機磁碟中建立最新版本的本機副本，且會移除檔案的唯讀屬性。 在某些情況下，您可能需要在未簽出檔案的情況下編輯檔案。 如需有關如何在未簽出檔案的情況下編輯檔案的詳細資訊，請參閱[編輯 Checked-In 檔案](../../2014/database-engine/edit-checked-in-files.md)。  
  
 您可以使用[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]手動或自動簽出檔案。 您以手動方式簽出檔案所開啟的方案中的檔案所在[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]環境，然後按一下**簽出**命令。 如果您設定 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 環境來自動簽出檔案，您也可以自動簽出檔案。  
  
 隨著管理員所設定的原始檔控制提供者的選項而不同，您也可以利用獨佔或共用模式來簽出檔案。 當您以獨佔模式簽出檔案時，只有您可以修改它，且在您重新簽入此檔案之前，任何其他使用者都無法將其簽出。 當您以共用模式簽出檔案時，其他使用者仍可簽出相同的檔案且使用者人數不限。 由於每位使用者都簽入檔案，因此，原始檔控制提供者會嘗試將檔案和檔案的最新伺服器版本合併起來。 如果簽入的版本與最新的版本發生衝突，原始檔控制提供者會提示使用者解決衝突。  
  
 下表描述此章節的主題。  
  
|主題|描述|  
|-----------|-----------------|  
|[簽出檔案](../../2014/database-engine/check-out-files.md)|提供如何簽出檔案以便修改的指示。|  
|[復原簽出](../../2014/database-engine/undo-checkouts.md)|說明如何取消現有的簽出。|  
|[在編輯時自動簽出檔案](../../2014/database-engine/automatically-check-out-files-upon-edit.md)|說明如何將原始檔控制設定成在開始編輯檔案時簽出檔案。|  
  
## <a name="see-also"></a>另請參閱  
 [管理簽入](../../2014/database-engine/manage-checkins.md)   
 [編輯簽入的檔案](../../2014/database-engine/edit-checked-in-files.md)  
  
  
