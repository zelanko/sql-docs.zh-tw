---
title: 使用 SQL Server Management Studio 在 SSIS 伺服器上執行封裝 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 56dc1bf8-99d4-41dc-bdc4-f64f1ccfd688
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a598030000e5764cecc8ababa75ef2bdd8598ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056383"
---
# <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 在 SSIS 伺服器上執行套件
  將專案部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器之後，即可在伺服器上執行封裝。  
  
 您可以使用作業報表，檢視已在伺服器上執行過或目前正在執行之封裝的相關資訊。 如需詳細資訊，請參閱 [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md)。  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 在伺服器上執行封裝  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 並連接至包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 目錄的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 執行個體。  
  
2.  依序展開 [物件總管] 中的 **[Integration Services 目錄]** 節點和 **[SSISDB]** 節點，然後導覽至已部署之專案中包含的封裝。  
  
3.  以滑鼠右鍵按一下封裝名稱，然後選取 [執行]****。  
  
4.  使用 [**執行封裝**] 對話方塊之 [**參數**]、[**連線管理員**] 和 [**高級**] 索引標籤上的設定，設定封裝執行。  
  
5.  按一下 **[確定]** 以執行封裝。  
  
     -或-  
  
     使用預存程序來執行封裝。 按一下 [指令碼]****，產生用以建立執行之執行個體與啟動執行之執行個體的 Transact-SQL 陳述式。 此陳述式包含了對 catalog.create_execution、catalog.set_execution_parameter_value 和 catalog.start_execution 預存程序的呼叫。 如需這些預存程序的詳細資訊，請參閱 [catalog.create_execution &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database)、[catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) 和 [catalog.start_execution &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)。  
  
  
