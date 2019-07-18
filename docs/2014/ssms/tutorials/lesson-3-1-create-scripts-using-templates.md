---
title: 建立使用範本的指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ed48014c-3fc9-48ff-8c0f-8d1822195f14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8387cdaf85d6fd7750229fda86c8cb3122b61d90
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913549"
---
# <a name="create-scripts-using-templates"></a>利用範本建立指令碼
  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供大量包含許多一般工作的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式之指令碼範本。 這些範本包含使用者提供值的參數，如資料表名稱。 您可以利用這些參數，只輸入名稱一次，之後，便自動將名稱複製到指令碼內所有必要的位置。 您可以撰寫您自己的自訂範本來支援您最常撰寫的指令碼。 您也可以重新組織範本樹狀結構、移動範本，或建立新資料夾來存放範本。 在下列練習中，您將利用範本，指定定序範本來建立資料庫。  
  
## <a name="using-templates"></a>使用範本  
  
#### <a name="to-create-a-script-using-a-template"></a>若要利用範本建立指令碼  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]的 [檢視]  功能表上，按一下 [範本總管]  。  
  
2.  [範本總管] 中的範本會組織成不同的群組。 展開 [資料庫]  ，然後按兩下 [建立資料庫]  。  
  
3.  在 [連接到 Database Engine]  對話方塊中，填妥連接資訊，然後按一下 [連接]  。 此時會開啟一個新的 [查詢編輯器] 視窗，其中含有 [建立資料庫]  範本的內容。  
  
4.  在 **[查詢]** 功能表上，按一下 **[指定範本參數的值]** 。  
  
5.  在 [指定範本參數的值]  對話方塊中，[值]  資料行包含 **Database_Name** 參數的建議值。 在 [資料庫名稱]  參數方塊中，輸入 [行銷]  ，然後按一下 [確定]  。 請注意在不同位置將 [行銷] 插入指令碼的方式。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立自訂範本](lesson-3-2-create-custom-templates.md)  
  
  
