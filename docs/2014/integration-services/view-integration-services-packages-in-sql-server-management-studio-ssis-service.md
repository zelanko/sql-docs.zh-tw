---
title: 檢視 Integration Services 封裝，在 SQL Server Management Studio （SSIS 服務） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- viewing packages
- connections [Integration Services], packages
ms.assetid: 783e653c-0f1f-45ed-b3ef-5ba07b019f27
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0d8196a46437975a2b8e00bb2fbe8d183540025c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054604"
---
# <a name="view-integration-services-packages-in-sql-server-management-studio-ssis-service"></a>在 SQL Server Management Studio 中檢視 Integration Services 封裝 (SSIS 服務)
    
> [!IMPORTANT]  
>  本主題會討論 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
 此程序描述如何在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中連接到 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ，以及檢視 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務所管理的封裝清單。  
  
### <a name="to-connect-to-integration-services"></a>連接到 Integration Services  
  
1.  按一下 **[開始]** ，依序指向 **[所有程式]** 和 **[Microsoft SQL Server]** ，然後按一下 **[SQL Server Management Studio]** 。  
  
2.  在 [連接到伺服器]  對話方塊中，選取 [伺服器類型]  清單中的 [Integration Services]  ，在 [伺服器名稱]  方塊中提供伺服器名稱，然後按一下 [連接]  。  
  
    > [!IMPORTANT]  
    >  如果您無法連接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務目前可能沒有執行。 若要了解此服務的狀態，請按一下 **[開始]** ，依序指向 **[所有程式]** 、 **[Microsoft SQL Server]** 和 **[組態工具]** ，然後按一下 **[SQL Server 組態管理員]** 。 在左窗格中，按一下 **[SQL Server 服務]** 。 在右窗格中，尋找 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務。 如果此服務尚未執行，請將它啟動。  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 隨即開啟。 依預設，[物件總管] 視窗會在 Studio 左下角開啟並定位。 如果 [物件總管] 未開啟，請按一下 **[檢視]** 功能表上的 **[物件總管]** 。  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>若要檢視 Integration Services 服務所管理的封裝  
  
1.  在 [物件總管] 中，展開 [存放的封裝] 資料夾。  
  
2.  展開 [Stored Packages] 的子資料夾以顯示封裝。  
  
## <a name="see-also"></a>另請參閱  
 [封裝管理 &#40;SSIS 服務&#41;](service/package-management-ssis-service.md)   
 [使用 SQL Server Management Studio](../database-engine/use-sql-server-management-studio.md)  
  
  
