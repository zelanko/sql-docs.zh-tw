---
title: 新增模型頁面 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 27d5bf66-b0e7-489e-a830-ffe2ec8e5350
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: df14375ad8ae54377f7dbbd599d0bcc7b50aa2d6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010789"
---
# <a name="new-model-page-report-manager"></a>新增模型頁面 (報表管理員)
  您可以使用這個頁面，從共用資料來源產生預設報表模型。 您只能從 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多維度資料來源、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 關聯式資料來源和 Oracle 關聯式資料來源產生報表模型。  
  
 您在報表管理員中產生的模型是以共用資料來源的結構描述為基礎。 系統會針對資料來源中的所有資料表和資料行建立實體、資料夾和欄位。 您無法排除這些項目，也無法設定決定模型產生方式的選項。 如果您想要自訂或修改模型，就必須改用模型設計師。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-new-model-page"></a>若要開啟新增模型頁面  
  
1.  開啟報表管理員，然後找出您想要從中產生模型的共用資料來源。  
  
2.  將滑鼠停留在該資料來源上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，執行下列其中一項步驟：  
  
    -   按一下 **[產生報表模型]** 開啟 [新增模型] 頁面。  
  
    -   按一下 **[管理]** 開啟報表的 [一般] 屬性頁面。 然後，按一下 **[產生報表模型]** 開啟 [新增模型] 頁面。  
  
## <a name="options"></a>選項。  
 **名稱**  
 指定模型的名稱。 名稱必須至少包含一個英數字元。 它也可以包含空格和某些符號。 指定名稱時，請勿使用下列字元：  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **說明**  
 顯示模型的描述。 透過報表管理員檢視這個項目的使用者會在瀏覽資料夾階層時看到此描述。  
  
 **變更位置**  
 顯示新模型的資料夾位置。 您可以按一下 **[變更位置]** 按鈕以選取不同的位置。  
  
  
