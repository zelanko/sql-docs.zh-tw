---
title: "連接到 Excel 活頁簿 |Microsoft 文件"
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel [Integration Services]
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b36b92c9beb840f6a2ea66250a5a025aa587acef
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-excel-workbook"></a>連接至 Excel 活頁簿
  若要將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝連接至 Microsoft Office Excel 活頁簿，您需要使用 Excel 連線管理員。  
  
 您可以從 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 的 [連線管理員] 區域或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈建立這些連線管理員。  
  
 **Microsoft Excel 和 Access 檔案的提供者和驅動程式**  
  
 如果尚未安裝 Microsoft Office 檔案的 OLE DB 提供者及驅動程式，您必須加以下載。 新版的提供者可以開啟以舊版 Excel 建立的檔案。  
  
 如果電腦有 32 位元版本的 Office，則必須安裝 32 位元版本的驅動程式，而且您也必須確定已執行精靈或以 32 位元模式建立的 Integration Services 封裝。  
  
|Microsoft Office 版本|下載|  
|------------------------------|--------------|  
|2007|[2007 Office System 驅動程式：資料連接元件](https://www.microsoft.com/en-us/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 執行階段](https://www.microsoft.com/en-us/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 執行階段](http://www.microsoft.com/en-us/download/details.aspx?id=39358)|  
  
### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>若要從連接管理員區域建立 Excel 連接管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟封裝。  
  
2.  在 [Connections Managers (連線管理員)] 區域中，以滑鼠右鍵按一下該區域中的任何位置，然後選取 [新增連線]。  
  
3.  在 [加入 SSIS 連線管理員] 對話方塊中，選取 [Excel]，然後設定連線管理員。  
  
     如需適用於這個連線管理員之組態選項的詳細資訊，請參閱 [Excel 連線管理員編輯器](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>若要從 SQL Server 匯入和匯出精靈建立 Excel 連接  
  
1.  啟動 32 位元版本的 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。  
  
2.  在 [選擇資料來源] 頁面中，針對 [資料來源] 選取 [Microsoft Excel]，然後設定 Excel 連接。  
  
     如需適用於這個連接類型之組態選項的詳細資訊，請參閱 [Excel 連線管理員編輯器](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [連接至 Access 資料庫](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  
