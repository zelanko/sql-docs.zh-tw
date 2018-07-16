---
title: Excel 連線管理員編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelconnection.f1
helpviewer_keywords:
- Excel Connection Manager Editor
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
caps.latest.revision: 27
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8c7a601344f28f99a31adb9d635c44e9cca85471
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287634"
---
# <a name="excel-connection-manager-editor"></a>Excel 連接管理員編輯器
  使用 [Excel 連線管理員編輯器] 對話方塊，將連接加入現有或新的 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 活頁簿檔案。  
  
 若要深入了解快取連線管理員，請參閱 [Excel 連線管理員](connection-manager/excel-connection-manager.md)。  
  
> [!NOTE]  
>  您不能連接到受密碼保護的 Excel 檔案。  
  
## <a name="options"></a>選項。  
 **Excel 檔案路徑**  
 輸入現有或新的 Excel 活頁簿檔案 (.xls) 的路徑和檔案名稱。  
  
> [!WARNING]  
>  **Excel 目的地編輯器**會自動建立 Excel 檔案，當您選取**Excel 連接**指向新/非現存檔案，然後按一下**新增**的**Excel 工作表名稱**。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊導覽至 Excel 檔存在的資料夾，或您要建立新的檔案。  
  
 **Excel 版本**  
 指定用於建立檔案的 Microsoft Excel 版本。  
  
|選項|描述|  
|------------|-----------------|  
|Excel 97-2003|檔案是使用 Excel 97 或更新版本建立的。|  
|Excel 3.0|使用 Excel 3.0 建立檔案。|  
|Excel 4.0|檔案是使用 Excel 4.0 建立的。|  
|Excel 5.0|檔案是使用 Excel 95 (7.0) 建立的。|  
  
 **第一個資料列有資料行名稱**  
 指定選取之工作表中資料的第一個資料列是否包含資料行名稱。 此選項的預設值是 **[True]**。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [使用 Foreach 迴圈容器來執行 Excel 檔案和資料表迴圈](control-flow/foreach-loop-container.md)  
  
  
