---
title: Excel 連線管理員 | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fdac3f09fa3b92d7babd9c43f5a71adc4191ac7e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923714"
---
# <a name="excel-connection-manager"></a>Excel 連接管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Excel 連線管理員可讓套件連接至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 活頁簿檔案。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 Excel 來源和 Excel 目的地使用 Excel 連線管理員。  
 
> [!IMPORTANT]
> 如需連接至 Excel 檔案，以及將資料從 Excel 檔案載入或載入至 Excel 檔案的限制與已知問題的詳細資訊，請參閱[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)。

 當您將 Excel 連線管理員加入封裝時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立一個連線管理員 (該連線管理員在執行階段會被解析為 Excel 連接)、設定連線管理員屬性，並將該連線管理員加入封裝上的 **Connections** 集合。  
  
 連線管理員的 **ConnectionManagerType** 屬性會設為 [EXCEL]  。  
  
## <a name="configure-the-excel-connection-manager"></a>設定 Excel 連線管理員  
 您可以利用下列方式設定 Excel 連接管理員：  
  
-   指定 Excel 活頁簿檔案的路徑。  
  
-   指定用於建立檔案的 Excel 版本。  
  
-   指出所選取工作表或範圍中第一個資料列是否包含資料行名稱。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中設定之屬性的詳細資訊，請參閱 [Excel 連線管理員編輯器](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="excel-connection-manager-editor"></a>Excel 連接管理員編輯器
  使用 [Excel 連線管理員編輯器]  對話方塊，將連接加入現有或新的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 活頁簿檔案。  
  
### <a name="options"></a>選項。  
 **Excel 檔案路徑**  
 輸入現有或新的 Excel 活頁簿檔案的路徑和檔案名稱。  
   
 **瀏覽**  
 使用 [開啟]  對話方塊巡覽至 Excel 檔存在的資料夾，或您要建立新檔案之處。  
  
 **Excel 版本**  
 指定用於建立檔案的 Microsoft Excel 版本。  
  
 **第一個資料列有資料行名稱**  
 指定選取之工作表中資料的第一個資料列是否包含資料行名稱。 此選項的預設值是 **[True]** 。  

## <a name="solution-to-import-data-with-mixed-data-types-from-excel"></a>從 Excel 匯入包含混合資料類型資料的解決方案

根據預設，如果您使用的資料包含混合資料類型，Excel 驅動程式會讀取前 8 列 (由 **TypeGuessRows** 登錄機碼設定)。 Excel 驅動程式會嘗試根據前 8 列，猜測每欄的資料類型。 例如，如果您的 Excel 資料來源在一欄中有數字與文字，若前 8 欄包含數字，則驅動程式可能會根據前 8 列，判斷欄中的資料是整數類型。 在此情況下，SSIS 會略過文字值，並將它們作為 NULL 匯入到目的地中。

若要解決此問題，請嘗試下列其中一個解決方案：

* 將 Excel 欄類型變更為 Excel 檔案中的**文字**。
* 將 IMEX 擴充屬性新增至連接字串，以覆寫驅動程式的預設行為。 當您將 ";IMEX = 1" 擴充屬性加入至連接字串的結尾時，Excel 會將所有資料視為文字。 請參閱下列範例：
    
  ```ACE OLEDB connection string:
  Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\ExcelFileName.xlsx;Extended Properties="EXCEL 12.0 XML;HDR=YES;IMEX=1";
  ```

   為了讓此解決方案可靠地運作，您可能還必須修改登錄設定。 main.cmd 檔案如下所示：
  
   ```cmd
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   ```

* 以 CSV 格式儲存檔案，並變更 SSIS 套件以支援 CSV 匯入。

## <a name="related-tasks"></a>相關工作  
[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)  
[Excel 來源](../data-flow/excel-source.md)  
[Excel 目的地](../data-flow/excel-destination.md)
