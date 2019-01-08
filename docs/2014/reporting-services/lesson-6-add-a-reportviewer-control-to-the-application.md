---
title: 第 6 課：將 ReportViewer 控制項新增至應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cf11d44179dadbc3362c2fcf6f946c30d6856a56
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53361120"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>第 6 課：將 ReportViewer 控制項加入至應用程式
  使用 [報表精靈] 設計子報表之後，下一步是要將 ReportViewer 控制項加入至網站應用程式。  
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>若要將 ReportViewer 控制項加入至應用程式  
  
1.  在**方案總管**中，以滑鼠右鍵按一下 **Default.aspx**，然後按一下 [檢視表設計師]。  
  
2.  從**AJAX Extensions**群組中**工具箱**視窗中，拖曳**ScriptManager**控制項至設計介面。  
  
3.  從 [報表] 群組，將 **ReportViewer** 控制項拖曳至設計介面上的 **ScriptManager** 控制項下方。  
  
4.  按一下 **ReportViewer** 控制項右上角的箭頭，開啟 [ReportViewer 工作] 視窗。  
  
5.  在 **選擇報表**方塊中，選取您建立的父報表。  
  
     當您選取報表時，報表中所使用的資料來源執行個體會自動建立。 產生的程式碼會具現化每個 DataTable (及其 [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) 容器)。 [ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource\(v=vs.100\).aspx) 控制項會新增至設計介面，對應報表中使用的每個資料來源。 此資料來源控制項會自動設定。  
  
     如果您使用 Microsoft Visual Studio 2012，請確定如果完整的名稱會列在其中將 ObjectDataSource 控制項結合完整專案命名空間的 dataset1**選擇您的商務物件**下拉式清單方塊 (例如 Projectnamespace.DataSet1TableAdapters.ProductTableAdapter)。 您以滑鼠右鍵按一下 [ObjectDataSource]，然後按一下 [存取] 清單方塊**設定資料來源**。  
  
6.  在 [建置] 功能表上，按一下 [建置網站]。  
  
     報表會進行編譯，而報表運算式中的任何錯誤 (像是語法錯誤) 都會出現在 [錯誤清單] 區域中。 按一下 Visual Studio 視窗底部的 [錯誤清單]，顯示 [錯誤清單] 區域。  
  
## <a name="next-task"></a>下一項工作  
 您已成功將 ReportViewer 控制項加入至網站應用程式。 接下來您將在父報表上加入鑽研動作。  
  
  
