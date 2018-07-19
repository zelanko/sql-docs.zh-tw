---
title: 一般屬性頁面，資料夾 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 31d99d9b-2303-4bae-9466-fb67b97cf11a
caps.latest.revision: 25
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4ee15c703cab10ced93359c91f170e7de0768e3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37255820"
---
# <a name="general-properties-page-folders-report-manager"></a>一般屬性頁面，資料夾 (報表管理員)
  使用資料夾的 [一般] 屬性頁面來檢視和設定您建立之資料夾的屬性。 有關誰建立和修改資料夾及何時修改資料夾的資訊顯示會在 [一般] 屬性頁面上方。  
  
 資料夾屬性也包含安全性設定。 如需有關資料夾安全性的詳細資訊，請參閱 <<c0> [ 保護資料夾的](security/secure-folders.md)。  
  
 不可以在報表伺服器命名空間內重新命名或移動特殊用途的資料夾 (例如，[主資料夾]、[我的報表] 和 [使用者] 資料夾)。 [一般] 屬性頁不適用於這些資料夾中。  
  
## <a name="navigation"></a>導覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
###### <a name="to-open-the-general-properties-page-for-a-folder"></a>若要開啟資料夾的一般屬性頁面  
  
1.  開啟報表管理員，然後開啟您想要檢視或設定屬性的資料夾。  
  
2.  在資料夾橫幅底下的工具列中，按一下 **[資料夾設定]**。  
  
## <a name="options"></a>選項。  
 **名稱**  
 指定資料夾的名稱。 名稱必須至少包含一個英數字元。 它也可以包含空格和某些符號。 請勿使用 ; ? : @ & = +，$ * \< > |"或 / 來指定名稱。  
  
 **說明**  
 輸入資料夾內容的描述。 此描述會出現在有權存取此資料夾之使用者的 [內容] 頁面上。  
  
 **在清單檢視中隱藏**  
 選取這個選項可以對正在「報表管理員」中使用清單檢視模式的使用者隱藏資料夾。 清單檢視模式是瀏覽報表伺服器資料夾階層時的預設檢視格式。 在清單檢視中，項目名稱和描述會跨頁排列。 替代格式是詳細資料檢視。 詳細資料檢視會省略描述，但會包括項目的其他相關資訊。 雖然在清單檢視中可以隱藏項目，但在詳細資料檢視中則不行。 如果想要限制項目的存取，您必須建立角色指派。  
  
 **套用**  
 按一下即可儲存您的變更。  
  
 **刪除**  
 按一下即可移除資料夾及其內容。  
  
 **[移動]**  
 按一下即可在報表伺服器命名空間中重新定位報表或資料夾。 按一下此按鈕會開啟 [移動項目] 頁面，您可在此瀏覽資料夾的新位置。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員&#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
