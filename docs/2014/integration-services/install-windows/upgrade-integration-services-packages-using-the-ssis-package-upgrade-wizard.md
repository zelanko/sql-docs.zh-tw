---
title: 使用 SSIS 封裝升級精靈來升級 Integration Services 封裝 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, upgrading
- upgrading Integration Services packages
ms.assetid: 9359275a-48f5-4d1e-8ae7-e797759e3ccf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e44b755748dcbda6af30e0570b667f9ba3ee75a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767883"
---
# <a name="upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard"></a>使用 SSIS 封裝升級精靈來升級 Integration Services 封裝
  您可以升級以舊版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所建立的封裝，至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所使用的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 格式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝升級精靈] 協助完成此程序。 因為您可以將精靈設定成備份原始封裝，所以如果您遇到升級問題，就可以繼續使用原始封裝。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝升級精靈是在安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 時安裝的。  
  
> [!NOTE]  
>  您可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 的 Standard、Enterprise 和 Developer Edition 中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]封裝升級精靈。  
  
 如需如何升級 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的詳細資訊，請參閱 [升級 Integration Services 封裝](upgrade-integration-services-packages.md)。  
  
 本主題的其餘部分描述的是如何執行此精靈以及備份原始封裝。  
  
## <a name="running-the-ssis-package-upgrade-wizard"></a>執行 SSIS 封裝升級精靈  
 您可以從 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 、從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]或在命令提示字元中執行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]封裝升級精靈。  
  
#### <a name="to-run-the-wizard-from-sql-server-data-tools"></a>若要從 SQL Server 資料工具執行此精靈  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，建立或開啟 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [SSIS 封裝]  節點，然後按一下 [升級所有封裝]  ，即可升級這個節點底下的所有封裝。  
  
    > [!NOTE]  
    >  當您開啟包含 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 封裝的 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 專案時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會自動開啟 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝升級精靈。  
  
#### <a name="to-run-the-wizard-from-sql-server-management-studio"></a>從 SQL Server Management Studio 執行此精靈  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，展開 [存放的封裝]  節點，以滑鼠右鍵按一下 [檔案系統]  或 [MSDB]  節點，然後按一下 [升級封裝]  。  
  
#### <a name="to-run-the-wizard-at-the-command-prompt"></a>在命令提示字元中執行此精靈  
  
-   在命令提示字元中，從**C:\Program FILES\MICROSOFT SQL Server\120\DTS\Binn**資料夾執行 ssisupgrade.exe 檔。  
  
## <a name="backing-up-the-original-packages"></a>備份原始封裝  
 若要備份原始封裝，原始封裝和升級封裝都必須存放在檔案系統的相同資料夾中。 根據您執行此精靈的方式，系統可能會自動選取這個儲存位置。  
  
-   當您從 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 執行 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]封裝升級精靈時，此精靈會自動將原始封裝和升級封裝都存放在檔案系統的相同資料夾中。  
  
-   當您從 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 或在命令提示字元中執行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 封裝升級精靈時，就可以針對原始和升級封裝指定不同的儲存位置。 若要備份原始封裝，請務必指定原始封裝和升級封裝都存放在檔案系統的相同資料夾中。 如果您指定任何其他儲存選項，此精靈將無法備份原始封裝。  
  
 當此精靈備份原始封裝時，它會將原始封裝的複本存放在 [SSISBackupFolder]  資料夾中。 此精靈會將這個 [SSISBackupFolder]  資料夾建立為包含原始封裝和升級封裝之資料夾的子資料夾。  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-management-studio-or-at-the-command-prompt"></a>在 SQL Server Management Studio 或命令提示字元中備份原始封裝  
  
1.  將原始封裝儲存到檔案系統上的位置。  
  
    > [!NOTE]  
    >  此精靈中的備份選項只能搭配已經存放至檔案系統的封裝運作。  
  
2.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或命令提示字元中，執行 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝升級精靈]。  
  
3.  在此精靈的 [選取來源位置]  頁面上，將 [封裝來源]  屬性設定為 [檔案系統]  。  
  
4.  在此精靈的 [選取目的地位置]  頁面上，選取 [儲存至來源位置]  ，即可將升級封裝儲存至與原始封裝相同的位置。  
  
    > [!NOTE]  
    >  只有當升級封裝與原始封裝都存放在相同的資料夾時，您才能使用此精靈的備份選項。  
  
5.  在此精靈的 [選取封裝管理選項]  頁面上，選取 [備份原始封裝]  選項。  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-data-tools"></a>若要在 SQL Server 資料工具中備份原始封裝  
  
1.  將原始封裝儲存到檔案系統上的位置。  
  
2.  在此精靈的 [選取封裝管理選項]  頁面上，選取 [備份原始封裝]  選項。  
  
    > [!WARNING]  
    >  當您在中[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]開啟或專案時，不會顯示 [**備份原始封裝**] 選項，而這會自動啟動精靈。  
  
3.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，執行 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝升級精靈。  
  
  
