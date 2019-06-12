---
title: 建立連結的報表 | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 77590da41aa09f66d7549a0d7ff615cdb3f63af3
ms.sourcegitcommit: 561cee96844b82ade6cf543a228028ad5c310768
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66506637"
---
# <a name="create-a-linked-report"></a>建立連結報表
  連結報表是提供現有報表之存取點的報表伺服器項目。 它在概念上類似於您用來執行程式或開啟檔案的程式捷徑。  
  
 連結報表是從現有的報表衍生，並保留原始的報表定義。 連結報表一律繼承原始報表的報表配置與資料來源屬性。 其他所有屬性與設定可以和原始報表不同，包括安全性、參數、位置、訂閱，以及排程。  
  
 您想要建立現有報表的其他版本時，可以建立連結報表。 例如，您可以使用單一區域銷售報表，來建立您所有銷售地區的區域特定報表。  
  
 雖然連結報表通常是以參數化報表為基礎，但參數化報表並不是必要的。 每當您想要以不同的設定部署現有的報表時，都可以建立連結報表。  
  
## <a name="to-create-a-linked-report"></a>若要建立連結報表  
  
1. 在入口網站中，瀏覽至所需的報表，以滑鼠右鍵按一下它，然後選取**管理**從下拉式清單。

2. 在 **管理<reportname>** 頁面上，選取**建立連結的報表**。  
  
3. 輸入新連結報表的名稱。 選擇性地輸入描述。  
  
4. 若要選取報表的其他資料夾，選取 右邊的省略符號按鈕 （...）***位置***。  瀏覽至報表，然後選取新資料夾**選取**。 如果您未選取不同的資料夾，則建立連結的報表是在目前的資料夾。  
  
5. 選取 [建立]  。 會建立連結的報表。  

6. 底下**進階**，選取不同**報表逾時**值，如有需要，然後選取**套用**以儲存變更。
  
     連結報表的圖示與報表伺服器所管理的其他項目不同。 下列圖示表示連結報表：  
  
     ![連結報表圖示](../../reporting-services/report-server/media/hlp-16linked.gif "連結報表圖示")  
  
## <a name="see-also"></a>另請參閱  
 [開啟及關閉報表&#40;web 入口網站&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)  
 [Reporting Services 概念 &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)  
 [報表伺服器的入口網站 (SSRS 原生模式)](../../reporting-services/web-portal-ssrs-native-mode.md)
  
