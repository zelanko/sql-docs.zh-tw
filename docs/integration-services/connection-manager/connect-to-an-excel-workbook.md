---
title: 連線至 Excel 活頁簿 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Excel [Integration Services]
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 62c9d7b4de0b764ff7208b0fa077ec12b58dec60
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-an-excel-workbook"></a>連接至 Excel 活頁簿
  若要將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝連接至 Microsoft Office Excel 活頁簿，您需要使用 Excel 連線管理員。  
  
 您可以從 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 的 [連線管理員] 區域或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈建立這些連線管理員。  
 
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Microsoft Excel 和 Access 檔案的連線元件
  
您可能必須下載 Microsoft Office 檔案的連線元件 (如果尚未安裝)。 在這裡下載 Excel 和 Access 檔案的連線元件最新版本：[Microsoft Access Database Engine 2016 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
最新版的元件可以開啟舊版 Excel 所建立的檔案。

如果電腦有 32 位元版本的 Office，則必須安裝 32 位元版本的元件，而且您也必須確定以 32 位元模式執行封裝。

如果您有 Office 365 訂用帳戶，請確定下載 Access Database Engine 2016 可轉散發套件，而非 Microsoft Access 2016 Runtime。 當您執行安裝程式時，可能會看到錯誤訊息，指出您無法使用 Office 隨選即用元件並存安裝下載。 若要略過此錯誤訊息並順利安裝元件，請開啟 [命令提示字元] 視窗並執行使用 `/quiet` 參數所下載的 .EXE 檔案，以無訊息模式執行安裝。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="create-an-excel-connection-manager"></a>建立 Excel 連線管理員

### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>若要從連接管理員區域建立 Excel 連接管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟封裝。  
  
2.  在 [Connections Managers (連線管理員)] 區域中，以滑鼠右鍵按一下該區域中的任何位置，然後選取 [新增連線]。  
  
3.  在 [加入 SSIS 連線管理員] 對話方塊中，選取 [Excel]，然後設定連線管理員。  
  
     如需適用於這個連線管理員之組態選項的詳細資訊，請參閱 [Excel 連線管理員編輯器](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>若要從 SQL Server 匯入和匯出精靈建立 Excel 連接  
  
1.  啟動 32 位元版本的 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。  
  
2.  在 [選擇資料來源] 頁面中，針對 [資料來源] 選取 [Microsoft Excel]，然後設定 Excel 連接。  
  
     如需適用於這個連接類型之組態選項的詳細資訊，請參閱 [Excel 連線管理員編輯器](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
## <a name="see-also"></a>另請參閱  
 [連接至 Access 資料庫](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  
