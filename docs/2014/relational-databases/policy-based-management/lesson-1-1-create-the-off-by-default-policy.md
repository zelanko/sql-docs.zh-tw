---
title: 建立 Off By Default 原則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 98fde3c5-297c-4d95-981e-95700bbf5ccd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 73294cfc5d1a7e4b2693615692604ef991421169
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117908"
---
# <a name="create-the-off-by-default-policy"></a>建立依預設為關閉的原則
  這項工作會建立名為 Mail Off 並且以介面區組態 Facet 為基礎的條件。 然後，它會建立名為 Off By Default 的原則。  
  
### <a name="to-create-the-mail-off-condition"></a>建立 Mail Off 條件  
  
1.  在物件總管中，依序展開 [管理]、[原則管理] 和 [Facet]、以滑鼠右鍵按一下 [介面區組態]，然後按一下 [新增條件]。  
  
2.  在 [建立新條件] 對話方塊的 [名稱] 方塊中，輸入 **Mail Off**。  
  
3.  在 [Facet] 方塊中，確認已選取 [介面區組態] Facet。  
  
4.  在 [運算式] 區域的 [欄位] 方塊中，選取 [@DatabaseMailEnabled]、在 [運算子] 方塊中選取 [=]，然後在 [值] 中選取 [False]。  
  
5.  在 [描述] 頁面上，輸入條件的描述，然後按一下 [確定] 建立條件。  
  
### <a name="to-create-the-off-by-default-policy"></a>建立 Off By Default 原則  
  
1.  在物件總管中，以滑鼠右鍵按一下 [介面區組態]，然後按一下 [新增原則]。  
  
2.  在 [建立新原則] 對話方塊的 [名稱] 方塊中，輸入 **Off By Default**。  
  
3.  將 [已啟用] 核取方塊保持不核取狀態。 [已啟用] 核取方塊會套用至自動原則，而且這個原則會視需要執行。  
  
4.  在 [檢查條件] 核取方塊中，向下捲動至 [介面區組態] 區域，然後選取 [Mail Off] 當作要檢查的條件。  
  
5.  [針對目標] 方塊將呈現空白，因為這是伺服器範圍的原則。  
  
6.  在 [評估模式] 核取方塊中，選取 [視需要] 當作評估模式。  
  
7.  在 [伺服器限制] 核取方塊中，選取 [無]。  
  
8.  在 [描述] 頁面上，輸入原則的描述。  
  
9. 您可以在 [其他說明超連結] 區域中，提供原則的網頁超連結。 在 [要顯示的文字] 方塊中，輸入要針對超連結顯示的文字。  
  
10. 在 [位址] 方塊中，輸入說明頁面的超連結，例如公司 IT 部門的首頁。  
  
11. 若要透過開啟網頁確認位址，請按一下 [測試連結]。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [將伺服器設定為執行 Off By Default 原則](lesson-1-2-configure-a-server-to-run-the-off-by-default-policy.md)  
  
  
