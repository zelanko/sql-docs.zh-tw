---
title: 指定連接字串 (SSAS) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.speconnstring.f1
ms.assetid: 3f89b55b-2659-4e9f-a3ad-ab9a23b6942d
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fc0988701ba21ef7e6880b85abab6309479a8a2f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136282"
---
# <a name="specify-a-connection-string-ssas"></a>指定連接字串 (SSAS)
  **[資料表匯入精靈]** 的這個頁面可讓您指定連接字串以連接至 OLE DB 或 ODBC 資料來源。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 若要連接至資料來源，您必須先在電腦上安裝適當的提供者。 如需支援的資料來源和提供者的詳細資訊，請參閱[支援的資料來源 &#40;SSAS 表格式&#41;](tabular-models/data-sources-supported-ssas-tabular.md)。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **此連接的易記名稱**  
 為此資料來源連接輸入唯一的名稱。 這是必要的欄位。  
  
 **連接字串**  
 輸入用來連接到 OLE DB 或 ODBC 資料來源的連接字串。  
  
 **建置**  
 使用 [資料連結屬性] 對話方塊，指定連接字串的屬性。 如需詳細資訊，請參閱可從該對話方塊存取的 Microsoft 資料連結說明。  
  
 **測試連接**  
 嘗試使用指定的連接字串，建立與資料來源之間的連接。 顯示一則訊息，指出連接是否成功。  
  
  