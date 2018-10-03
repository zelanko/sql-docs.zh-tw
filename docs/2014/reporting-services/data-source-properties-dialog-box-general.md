---
title: 資料來源屬性對話方塊、 一般 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.general.f1
- "10120"
ms.assetid: 44b5edd3-5c11-4d3d-91b8-5871aa0572ed
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7c99c1033472a58437913fe8a3356e0c3219075c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156378"
---
# <a name="data-source-properties-dialog-box-general"></a>資料來源屬性對話方塊、一般
  選取 **[資料來源屬性]** 對話方塊上的 **[一般]** ，即可在報表中顯示和修改資料來源的連接資訊。  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入資料來源的名稱。 資料來源名稱在報表內必須是唯一的。 根據預設，系統會將一般名稱 (例如，DataSource1 或 DataSource2) 指派給資料來源。  
  
 **內嵌的連接**  
 當您不想要使用共用資料來源時，選取此選項。  
  
 **型別**  
 選取資料處理延伸模組。 此清單會顯示所有已註冊的延伸模組。  
  
 **連接字串**  
 輸入資料來源的連接字串。 按一下 **[編輯]** ，即可使用 **[連接屬性]** 對話方塊來建立連接字串。 請按一下 [運算式] (*fx*) 按鈕來編輯運算式。  
  
 **使用共用的資料來源參考**  
 選取此選項即可連結至共用資料來源。 從下拉式清單選取共用資料來源。 若要編輯選取的資料來源，請按一下 **[編輯]**。 如果選取 **[使用共用資料來源參考]** ，就會停用 **[類型]** 和 **[連接字串]** 。  
  
 **處理查詢時，使用單一交易**  
 選取此選項，指出使用此資料來源的資料集會在單一交易中針對資料庫執行。 若要包含使用相同資料來源之子報表的交易，請在 **[屬性]** 窗格之子報表的 **[其他屬性]** 區段中，將 **MergeTransactions** 設定為 **True** 。  
  
## <a name="see-also"></a>另請參閱  
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [建立內嵌或共用資料來源&#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)   
 [資料連接、 資料來源和 Reporting Services 中的連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [資料來源屬性對話方塊，認證](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)  
  
  
