---
title: "開發自訂 ForEach 列舉值的使用者介面 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom user interface [Integration Services], custom foreach enumerators
- custom foreach enumerators [Integration Services], developing custom user interface
ms.assetid: 8aa4aa80-c9ba-42b3-ba87-ae5ea5d3cac3
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e743464fcf482ea51f0cde78d692b367c2be525b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-user-interface-for-a-custom-foreach-enumerator"></a>開發自訂 ForEach 列舉值的使用者介面
  在您已覆寫可提供自訂功能的基底類別之屬性與方法的實作之後，可能會想要針對 Foreach 列舉值建立自訂使用者介面。 如果您未建立自訂使用者介面，使用者可以使用 [屬性] 視窗來設定新的自訂 Foreach 列舉值。  
  
 在自訂的使用者介面專案或是組件中，您可以建立可實作 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI> 的類別。 此類別衍生自 System.Windows.Forms.UserControl，通常用來建立複合控制項，以主控其他 Windows Form 控制項。 建立控制項，會顯示在**列舉值組態**區域**集合** 索引標籤**Foreach 迴圈編輯器**。  
  
> [!IMPORTANT]  
>  在簽署和建置您的自訂使用者介面，以及安裝在全域組件快取中所述之後[建置、 部署及偵錯自訂物件](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)，請記得要提供此類別中的完整格式的名稱<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A>屬性<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>。  
  
## <a name="coding-the-user-interface-control-class"></a>撰寫使用者介面控制項類別的程式碼  
  
### <a name="initializing-the-user-interface"></a>初始化使用者介面  
 您會覆寫 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.Initialize%2A> 方法來快取主機物件的參考，以及連線管理員集合與定義在封裝中之變數的參考。  
  
### <a name="setting-properties-on-the-user-interface-control"></a>在使用者介面控制項上設定屬性  
 UserControl 類別，從其中衍生的使用者介面的類別，僅供做為複合控制項以主控其他 Windows Form 控制項。 因為這個類別會主控其他的控制項，所以您可以設計自訂使用者介面，方法是在任何 Windows Form 應用程式中，拖放控制項、排列它們、設定其屬性以及在執行階段回應其事件。  
  
### <a name="saving-settings"></a>節省設定  
 您會覆寫 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI.SaveSettings%2A> 方法，以便在使用者關閉編輯器時，從控制項將使用者選取的值複製到列舉值的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂 Foreach 列舉值](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)   
 [程式碼撰寫自訂 Foreach 列舉值](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
  
  
