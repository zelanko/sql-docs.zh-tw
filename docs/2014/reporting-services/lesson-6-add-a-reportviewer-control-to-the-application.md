---
title: 第 6 課：將 ReportViewer 控制項新增至應用程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dfce5e2bdf71dfb58481fedf05794d3603285449
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108415"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>第 6 課：將 ReportViewer 控制項加入到應用程式
  使用 [報表精靈] 設計子報表之後，下一步是要將 ReportViewer 控制項加入至網站應用程式。  
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>若要將 ReportViewer 控制項加入至應用程式  
  
1.  在**方案總管**中，以滑鼠右鍵按一下 **Default.aspx**，然後按一下 [檢視表設計師]****。  
  
2.  從 [**工具箱**] 視窗的 [ **AJAX 擴充**功能] 群組中，將**ScriptManager**控制項拖曳至設計介面。  
  
3.  從 [報表]**** 群組，將 **ReportViewer** 控制項拖曳至設計介面上的 **ScriptManager** 控制項下方。  
  
4.  按一下 **ReportViewer** 控制項右上角的箭頭，開啟 [ReportViewer 工作]**** 視窗。  
  
5.  在 [**選擇報表**] 方塊中，選取您建立的父報表。  
  
     當您選取報表時，報表中所使用的資料來源執行個體會自動建立。 產生的程式碼會具現化每個 DataTable (及其 [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) 容器)。 [ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource\(v=vs.100\).aspx) 控制項會新增至設計介面，對應報表中使用的每個資料來源。 此資料來源控制項會自動設定。  
  
     如果您使用 Microsoft Visual Studio 2012，請確定 ObjectDataSource 控制項已與專案命名空間完全符合的 DataSet1 系結（如果完整名稱列在 [**選擇您的商務物件**] 下拉式清單方塊中（例如，Projectnamespace. DataSet1TableAdapters. projectnamespace.dataset1tableadapters.producttableadapter）。 以滑鼠右鍵按一下 [ObjectDataSource]，然後按一下 [**設定資料來源**]，即可存取清單方塊。  
  
6.  在 [建置] 功能表上，按一下 [建置網站]。  
  
     報表會進行編譯，而報表運算式中的任何錯誤 (像是語法錯誤) 都會出現在 [錯誤清單]  區域中。 按一下 Visual Studio 視窗底部的 [錯誤清單]  ，顯示 [錯誤清單]  區域。  
  
## <a name="next-task"></a>下一項工作  
 您已成功將 ReportViewer 控制項加入至網站應用程式。 接下來您將在父報表上加入鑽研動作。  
  
  
