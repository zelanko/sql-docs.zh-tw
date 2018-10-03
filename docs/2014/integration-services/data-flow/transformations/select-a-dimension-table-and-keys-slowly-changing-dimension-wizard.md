---
title: 選取維度資料表與索引鍵 (緩時變維度精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 277802a17e58de6f74274c88cb065ac22ed951e3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200658"
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>選取維度資料表與索引鍵 (緩時變維度精靈)
  使用 **[選取維度資料表與索引鍵]** 頁面，即可選取要載入的維度資料表。 將資料流程的資料行對應至即將載入的資料行。  
  
 若要深入了解這個精靈，請參閱＜ [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **[ODBC 目的地編輯器]**  
 從清單中選取現有的 OLE DB 連線管理員，或按一下 [新增] 建立 OLE DB 連線管理員。  
  
> [!NOTE]  
>  [緩時變維度精靈] 只支援 OLE DB 連線管理員，所以只支援與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的連線。  
  
 **新增**  
 使用 [設定 OLE DB 連線管理員] 對話方塊，以選取現有的連線管理員，或按一下 [新增] 建立新的 OLE DB 連線。  
  
 **[資料表或檢視表]**  
 從清單中選取資料表或檢視。  
  
 **輸入資料行**  
 從輸入資料行的清單中選取您要指定對應的資料行。  
  
 **維度資料行**  
 檢視所有可用的維度資料行。  
  
 **索引鍵類型**  
 選取其中一個維度資料行作為商務索引鍵。 您必須要有一個商務索引鍵。  
  
## <a name="see-also"></a>另請參閱  
 [使用緩時變維度精靈來設定輸出](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
