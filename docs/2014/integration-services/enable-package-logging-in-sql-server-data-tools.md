---
title: 啟用封裝記錄功能在 SQL Server 資料工具 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], enabling
ms.assetid: b69a8593-5bb0-4f04-87d2-f8e7bd7eb4fc
caps.latest.revision: 42
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e0c34833bf458ce38a8e83a1a3db2a40f0760b2e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320668"
---
# <a name="enable-package-logging-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中啟用封裝記錄功能
  本程序描述如何將記錄檔加入封裝、設定封裝層級的記錄，以及將記錄組態儲存至 XML 檔案。 您可以僅在封裝層級加入記錄檔，但封裝無需執行記錄即可啟用封裝所包含之容器中的記錄。  
  
> [!IMPORTANT]  
>  如果您將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案部署到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器，則您為封裝執行設定的記錄層次會覆寫您使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]設定的封裝記錄。  
  
 依預設，封裝中的容器使用與其父容器相同的記錄組態。 如需設定個別容器之記錄選項的資訊，請參閱 [使用已儲存的組態檔來設定記錄](../../2014/integration-services/configure-logging-by-using-a-saved-configuration-file.md)。  
  
### <a name="to-enable-logging-in-a-package"></a>若要啟用封裝中的記錄  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 **[SSIS]** 功能表上，按一下 **[記錄]**。  
  
3.  在 [提供者類型] 清單中選取記錄提供者，然後按一下 [加入]。  
  
4.  在 [設定] 資料行中，選取連線管理員，或按一下 [\<新增連線>]，為記錄提供者建立適當類型的新連線管理員。 因所選提供者的不同，使用下列連接管理員之一：  
  
    -   若為「文字」檔案，請使用「檔案」連接管理員。 如需詳細資訊，請參閱 [檔案連線管理員](connection-manager/file-connection-manager.md)  
  
    -   若為 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]，請使用檔案連線管理員。  
  
    -   若為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請使用 OLE DB 連接管理員。 如需相關資訊，請參閱 [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md)。  
  
    -   若為 Windows 事件記錄檔，不需任何動作。 [!INCLUDE[ssIS](../includes/ssis-md.md)] 會自動建立記錄檔。  
  
    -   若為 XML 檔案，請使用「檔案」連接管理員。  
  
5.  針對封裝中要使用的每個記錄檔重複步驟 3 和 4。  
  
    > [!NOTE]  
    >  封裝可以使用每種類型一個以上的記錄檔。  
  
6.  選擇性地選取封裝層級核取方塊，並選取要用於封裝層級記錄的記錄檔，然後按一下 [詳細資料] 索引標籤。  
  
7.  在 [詳細資料] 索引標籤上，選取 [事件]，以記錄所有記錄項目，或清除 [事件]，以選取個別事件。  
  
8.  選擇性地按一下 [進階]，以指定要記錄哪些資訊。  
  
    > [!NOTE]  
    >  依預設，會記錄所有資訊。  
  
9. 在 [詳細資料] 索引標籤上，按一下 [儲存]。 [另存新檔] 對話方塊隨即出現。 尋找要儲存記錄組態的資料夾，輸入新記錄組態的檔案名稱，然後按一下 [儲存]。  
  
10. 按一下 [確定] 。  
  
11. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41;記錄](performance/integration-services-ssis-logging.md)   
 [Integration Services &#40;SSIS&#41; 記錄](performance/integration-services-ssis-logging.md)  
  
  
