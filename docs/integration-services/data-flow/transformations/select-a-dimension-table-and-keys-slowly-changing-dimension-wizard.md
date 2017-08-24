---
title: "選取維度資料表與索引鍵 （緩時變維度精靈） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 24413b539223f32d8ee808d584bb1a629f3f7e23
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>選取維度資料表與索引鍵 (緩時變維度精靈)
  使用 **[選取維度資料表與索引鍵]** 頁面，即可選取要載入的維度資料表。 將資料流程的資料行對應至即將載入的資料行。  
  
 若要深入了解這個精靈，請參閱＜ [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 **連線管理員**  
 從清單中選取現有的 OLE DB 連線管理員，或按一下 [新增] 建立 OLE DB 連線管理員。  
  
> [!NOTE]  
>  [緩時變維度精靈] 只支援 OLE DB 連線管理員，所以只支援與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的連線。  
  
 **新增**  
 使用 [設定 OLE DB 連線管理員] 對話方塊，以選取現有的連線管理員，或按一下 [新增] 建立新的 OLE DB 連線。  
  
 **資料表或檢視表**  
 從清單中選取資料表或檢視。  
  
 **輸入資料行**  
 從輸入資料行的清單中選取您要指定對應的資料行。  
  
 **維度資料行**  
 檢視所有可用的維度資料行。  
  
 **索引鍵類型**  
 選取其中一個維度資料行作為商務索引鍵。 您必須要有一個商務索引鍵。  
  
## <a name="see-also"></a>請參閱＜  
 [使用 「 緩時變更維度精靈 」 來設定輸出](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
