---
title: 部署專案之後設定參數值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: c9dcca4d-f1a0-45ec-b078-f4d372589baf
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5cb12795b0aba94da115916b2b09dc0c2675e8ba
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151801"
---
# <a name="set-parameter-values-after-the-project-is-deployed"></a>部署專案之後設定參數值
  部署精靈可讓您在將專案部署到目錄時，設定伺服器預設參數值。 專案在目錄中之後，您可以使用 SQL Server Management Studio (SSMS) 物件總管或 Transact-SQL 來設定伺服器預設值。  
  
### <a name="to-set-server-defaults-with-ssms-object-explorer"></a>若要使用 SSMS 物件總管來設定伺服器預設值，請執行下列作業：  
  
1.  選取並以滑鼠右鍵按一下 [Integration Services] 節點底下的專案。  
  
2.  按一下 **[屬性]** ，以開啟 **[專案屬性]** 對話方塊視窗。  
  
3.  按一下 **[選取頁面]** 底下的 **[參數]**，以開啟參數頁面。  
  
4.  在 **[參數]** 清單選取所需的參數。 附註： **[容器]** 資料行有助於區分專案參數與封裝參數。  
  
5.  在 **[值]** 資料行中，指定所需的伺服器預設參數值。  
  
 若要使用 Transact-SQL 設定伺服器預設值，請使用 [catalog.set_object_parameter_value &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database) 預存程序。 若要檢視目前的伺服器預設值，請查詢 [catalog.object_parameters &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database) 檢視。 若要清除伺服器預設值，請使用 [catalog.clear_object_parameter_value &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database) 預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41;參數](integration-services-ssis-package-and-project-parameters.md)  
  
  
