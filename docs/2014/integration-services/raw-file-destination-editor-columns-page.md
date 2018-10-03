---
title: 原始檔案目的地編輯器 （資料行頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfiledestinationcolumns.f1
ms.assetid: 37f61d0b-1269-42ee-94ab-011cbaac63e9
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f833084ea5faecaa7e494397e7f1651b3086e513
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095860"
---
# <a name="raw-file-destination-editor-columns-page"></a>原始檔案目的地編輯器 (資料行頁面)
  使用原始檔案目的地編輯器設定原始檔案目的地將，以便將原始資料寫入至檔案。  
  
 **您想要做什麼事？**  
  
-   [開啟原始檔案目的地編輯器](#open)  
  
-   [設定連接管理員索引標籤上的選項](#connection)  
  
-   [設定資料行索引標籤上的選項](#mapping)  
  
##  <a name="open"></a> 開啟原始檔案目的地編輯器  
  
1.  將「原始檔案」目的地加入至 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]封裝。  
  
2.  以滑鼠右鍵按一下此元件，然後按一下 **[編輯]**。  
  
##  <a name="connection"></a> 設定連接管理員索引標籤上的選項  
 **存取模式**  
 選取指定檔案名稱的方式。 選取 **[檔案名稱]** 直接輸入檔案名稱和路徑，或是選取 **[來自變數的檔案名稱]** 指定包含檔案名稱的變數。  
  
 **[檔案名稱]** 或 **[變數名稱]**  
 輸入原始檔案的名稱和路徑，或是選取包含檔案名稱的變數。  
  
 **寫入選項**  
 選取用來建立和寫入檔案的方法。  
  
 **產生初始的原始檔案**  
 按一下此按鈕可以產生僅包含資料行 (僅中繼資料的檔案) 的空白原始檔案，而不必執行封裝。 您可以將原始檔案來源指向僅中繼資料的檔案。  
  
 當您按一下該按鈕時，資料行的清單便會出現。 您可以按一下 [取消]，然後修改資料行，或按一下 [確定]，以繼續建立該檔案。  
  
##  <a name="mapping"></a> 設定資料行索引標籤上的選項  
 **可用的輸入資料行**  
 選取要寫入至原始檔案的一個或多個輸入資料行。  
  
 **輸入資料行**  
 當您在 **[可用的輸入資料行]** 底下選取資料表時，輸入資料行會自動加入此資料表中，或者您可以直接在此資料表中選取輸入資料行。  
  
 **輸出別名**  
 指定要做為輸出資料行使用的替代名稱。  
  
## <a name="see-also"></a>另請參閱  
 [原始檔案目的地](data-flow/raw-file-destination.md)  
  
  
