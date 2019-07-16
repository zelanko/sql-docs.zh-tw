---
title: 在 Excel 中使用的 BI 語意模型連接或 Reporting Services |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bfd1bde3a39af9954437c6f777d82db1f1ffe187
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163616"
---
# <a name="use-a-bi-semantic-model-connection-in-excel-or-reporting-services"></a>在 Excel 或 Reporting Services 使用 BI 語意模型連接
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本主題說明如何使用透過其他主題的指示所建立的 BI 語意模型連接。 如果您尚未建立 BI 語意模型，請參閱 [建立與 Power Pivot 活頁簿的 BI 語意模型連接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md) 和 [建立與表格式模型資料庫的 BI 語意模型連接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)。  
  
##  <a name="bkmk_connect"></a> 從 Excel 連接  
 您可以在 Excel 或是使用 Analysis Services 表格式模型資料的其他任何商務應用程式中，指定 BI 語意模型連接當做資料來源。 本節說明使用 Excel 連接到 BI 語意模型資料的兩種方法。  
  
 來自 Excel 的 BI 語意模型連接要求在工作站上安裝 Excel 2010 和 MSOLAP.5 OLE DB 提供者。 本節會進一步提供有關連接需求的其他資訊。  
  
 **從 SharePoint 啟動**  
  
-   以滑鼠右鍵按一下文件庫中的 BI 語意模型連接，然後選取 [啟動 Excel]  。  
  
 ![螢幕擷取畫面的 BISM 快速啟動命令](../../analysis-services/power-pivot-sharepoint/media/ssas-bism-quicklaunch.gif "螢幕擷取畫面的 BISM 快速啟動命令")  
  
 當系統提示您啟用資料連接時，按一下 **[啟用]** 。 Excel 會開啟活頁簿，其中包含填入了基礎資料來源中之欄位的樞紐分析表欄位清單。  
  
 **從 Excel 啟動**  
  
1.  啟動 Excel 並開啟活頁簿。 在 [資料] 索引標籤上，按一下 [取得外部資料] 中的 **[從其他來源]** 。  
  
2.  按一下 **[從 Analysis Services]** ，然後使用 [資料連線精靈] 匯入資料。  
  
3.  輸入 BI 語意模型連接檔案的 SharePoint URL (例如， `http://mysharepoint/shared documents/myData.bism`)。 接受認證選項 **[使用 Windows 驗證]** 上的預設記錄檔。 按一下 [下一步]  。  
  
4.  在下一個頁面上，再按 **[下一步]** 。 雖然系統會提示您選取資料庫，但是您只能使用在 BI 語意模型連接中指定的資料庫。  
  
5.  在最後一個頁面上，您可以提供易記名稱和描述。 按一下 **[完成]** ，然後按一下 [匯入資料] 對話方塊上的 **[確定]** 來匯入資料。  
  
 若要讓連接成功，您必須將 Excel 2010 和 MSOLAP.5.dll 安裝在用戶端電腦上。 您可以藉由安裝這個版本的目前 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 版本來取得提供者，或者可以從 [功能套件下載頁面](http://go.microsoft.com/fwlink/?linkid=214066)下載 Analysis Services OLE DB 提供者。  
  
 若要確認 MSOLAP.5.dll 是最新的版本，請檢查登錄中的 **HKEY_CLASSES_ROOT\MSOLAP** 。 **CurVer** 應該設定為 MSOLAP.5。  
  
 在 SharePoint 中，您也必須擁有 BI 語意模型檔案的「讀取」權限。 「讀取」權限包含下載權限。 Excel 會從 SharePoint 下載 BI 語意模型連接資訊，然後透過 **HTTP Get**開啟與資料庫的直接連接。 一旦 BI 語意模型連接資訊在本機上儲存，連接要求就不會流經 SharePoint。  
  
 如果您要連接至 Analysis Services 伺服器上執行的表格式模型資料庫，則 SharePoint 權限還不夠。 您也必須擁有伺服器的資料庫讀取權限。 當您建立 BI 語意模型連接時，應該已經執行這個步驟。 如需詳細資訊，請參閱 [建立與表格式模型資料庫的 BI 語意模型連接](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)。  
  
##  <a name="bkmk_use"></a> 在 SharePoint 中從 Reporting Services 連接  
 您可以利用您使用多數資料來源的相同方式來使用 BI 語意模型連接，方法是在使用資料的文件或工具中，將檔案指定為資料來源。 雖然 BI 語意模型連接會指向其他伺服器上的實體資料庫，但是您要將該連接檔案本身當做資料來源使用。 BI 語意模型連接的 SharePoint URL 對於使用 BI 語意模型資料的 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 報表而言是有效的資料來源位置。  
  
 針對 SharePoint 中的隨選報表設計，建立報表的使用者必須擁有 BI 語意模型連接 (.bism) 檔案和商業智慧語意模型資料庫的 SharePoint 權限。 連接的安全性內容是正在建立報表的互動式使用者。  
  
  
