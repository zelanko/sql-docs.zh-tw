---
title: 開發自訂 Foreach 列舉值的使用者介面 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8965fcda896c67b2ae2e08cde54c679e6504b8b6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896068"
---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>開發自訂 ForEach 列舉值的使用者介面
  在您已覆寫可提供自訂功能的基底類別之屬性與方法的實作之後，可能會想要針對 Foreach 列舉值建立自訂使用者介面。 如果您未建立自訂使用者介面，使用者可以使用 [屬性] 視窗來設定新的自訂 Foreach 列舉值。  
  
 在自訂的使用者介面專案或是組件中，您可以建立可實作 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI> 的類別。 這個類別衍生自 System.Windows.Forms.UserControl，通常它是用於建立複合控制項，以主控其他的 Windows Form 控制項。 在 **Foreach 迴圈編輯器**中，您建立的控制項是顯示在 [集合] 索引標籤的 [列舉值設定] 區域中。  
  
> [!IMPORTANT]  
>  在簽署和組建自訂使用者介面，以及在全域組件快取中安裝它之後 (如[建立、部署和偵錯自訂物件](../building-deploying-and-debugging-custom-objects.md)所述)，請記得在 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> 屬性中提供這個類別的完整名稱。  
  
## <a name="coding-the-user-interface-control-class"></a>撰寫使用者介面控制項類別的程式碼  
  
### <a name="initializing-the-user-interface"></a>初始化使用者介面  
 您會覆寫 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A> 方法來快取主機物件的參考，以及連線管理員集合與定義在封裝中之變數的參考。  
  
### <a name="setting-properties-on-the-user-interface-control"></a>在使用者介面控制項上設定屬性  
 衍生使用者介面類別的 UserControl 類別，是用來作為複合控制項以主控其他的 Windows Form 控制項。 因為這個類別會主控其他的控制項，所以您可以設計自訂使用者介面，方法是在任何 Windows Form 應用程式中，拖放控制項、排列它們、設定其屬性以及在執行階段回應其事件。  
  
### <a name="saving-settings"></a>節省設定  
 您會覆寫 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A> 方法，以便在使用者關閉編輯器時，從控制項將使用者選取的值複製到列舉值的屬性。  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂的 Foreach 列舉值](creating-a-custom-foreach-enumerator.md)   
 [撰寫自訂 Foreach 列舉程式的程式碼](coding-a-custom-foreach-enumerator.md)  
  
  
