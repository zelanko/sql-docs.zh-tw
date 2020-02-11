---
title: 新增連結報表頁面（報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fefb46e8-6901-4d50-a3f8-7c49ad72e7b1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b6aab8fc0c8e083181779c13654b0d7d42531e50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108172"
---
# <a name="new-linked-report-page-report-manager"></a>新增連結報表頁面 (報表管理員)
  使用 [新增連結報表] 頁面即可建立連結報表。 連結報表具有專屬的設定值和屬性，但連結至另一個報表的報表定義。 當您有想要針對特定群組或使用者改變的基底報表時，連結報表就很有用。例如，根據您指定為參數之區域碼傳回不同資料的區域報表。 通常是在變更參數化的報表時建立連結報表，然後以不同的參數值儲存每一個報表執行個體。 不過，可以從您有權存取的任何報表來建立連結報表。  
  
 連結報表可以有自己的名稱、描述、位置、參數屬性、報表執行屬性、報表記錄屬性、權限和訂閱。 不過，連結報表必須使用提供報表定義之基底報表的資料來源屬性和配置。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-new-linked-report-page-from-the-contents-page"></a>若要從內容頁面開啟新增連結報表頁面  
  
1.  開啟報表管理員，然後找出您想要建立連結報表的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[建立連結報表]**。  
  
###### <a name="to-open-the-new-linked-report-page-from-the-general-properties-page-of-a-report"></a>若要從報表的一般屬性頁面開啟新增連結報表頁面  
  
1.  開啟報表管理員，然後找出您想要建立連結報表的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]** 。 這樣就會開啟該報表的 [一般] 屬性頁面。  
  
4.  在項目工具列中，按一下 **[建立連結報表]**。  
  
## <a name="options"></a>選項。  
 **名稱**  
 指定連結報表的名稱。 名稱必須至少包含一個英數字元。 也可以包含空格和特定符號。 不過，您不可以使用 ; ? ： \@ & = +，$/* \< > |"或/指定名稱時。  
  
 **說明**  
 輸入報表內容的描述。 此描述顯示在有權存取此報表的使用者的 [內容] 頁面上。  
  
 **位置**  
 指定含有此報表的資料夾路徑。 在預設狀況下，建立的連結報表與基礎報表為同層級。 按一下 **[變更位置]** 即可將連結報表置於不同的資料夾中。  
  
 **確定**  
 按一下 **[確定]** 即可儲存變更，並回到基底報表的 [一般] 屬性頁面。  
  
## <a name="see-also"></a>另請參閱  
 [建立連結報表](reports/create-a-linked-report.md)   
 [一般屬性頁面、報表 &#40;報表管理員&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
