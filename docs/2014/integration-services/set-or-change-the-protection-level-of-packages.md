---
title: 設定或變更封裝的保護等級 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services],security
- security [Integration Services],protection levels
- protection level for packages [Integration Services]
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ae909a1f7a61c5ae2aa3d6319fd03c54dd70b0e1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421825"
---
# <a name="set-or-change-the-protection-level-of-packages"></a>設定或變更封裝的保護等級
  若要控制封裝內容以及其中包含之機密值 (例如密碼) 的存取權，請設定 `ProtectionLevel` 屬性的值 包含在專案中的封裝需要有和專案相同的保護層級，才能建立專案。 如果您變更專案上的 `ProtectionLevel` 屬性設定，就需要手動更新封裝的屬性設定。  
  
 如需如何在 `ProtectionLevel` 封裝生命週期的不同階段判斷封裝適用之設定的詳細資訊，請參閱封裝[中的敏感性資料存取控制](security/access-control-for-sensitive-data-in-packages.md)。 如需 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 安全性功能的概觀，請參閱[安全性概觀 &#40;Integration Services&#41;](security/security-overview-integration-services.md)。  
  
 本主題中的程序說明如何使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 或 dtutil 命令提示字元公用程式來變更 `ProtectionLevel` 屬性。  
  
> [!NOTE]  
>  除了本主題中的程序之外，您通常可以在匯入或匯出封裝時，設定或變更封裝的 `ProtectionLevel` 屬性。 您也可以在使用 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 匯入和匯出精靈] 來儲存封裝時，變更封裝的 `ProtectionLevel` 屬性。  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>若要在 SQL Server 資料工具中設定或變更封裝的保護等級  
  
1.  `ProtectionLevel`在[設定封裝的保護等級](security/access-control-for-sensitive-data-in-packages.md)主題中，檢查屬性的可用值，並決定您的封裝的適當值。  
  
2.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計器中，開啟封裝。  
  
4.  如果 [屬性] 視窗並未顯示封裝屬性，請按一下設計介面。  
  
5.  在 [屬性視窗的 [**安全**] 群組中，為屬性選取適當的值 `ProtectionLevel` 。  
  
     如果您選取了需要密碼的保護等級，請輸入密碼作為 **PackagePassword** 屬性的值。  
  
6.  在 [檔案]**** 功能表上，選取 [儲存選取項目]**** 以儲存修改過的封裝。  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>在命令提示字元設定或變更封裝的保護等級  
  
1.  `ProtectionLevel`在[設定封裝的保護等級](security/access-control-for-sensitive-data-in-packages.md)主題中，檢查屬性的可用值，並決定您的封裝的適當值。  
  
2.  `Encrypt`在[Dtutil 公用程式](dtutil-utility.md)主題中，檢查選項的對應，並判斷要當做所選屬性值使用的適當整數 `ProtectionLevel` 。  
  
3.  開啟命令提示字元視窗。  
  
4.  在命令提示字元，導覽至您要設定其 `ProtectionLevel` 屬性之封裝的所在資料夾。  
  
     下列步驟所示的語法範例假設此資料夾為目前的資料夾。  
  
5.  使用類似於下列其中一個範例的命令，設定或變更封裝的保護等級：  
  
    -   下列命令會將檔案系統中個別封裝的 `ProtectionLevel` 屬性設為層級 2「機密資料以密碼加密」，並且將密碼設為 "strongpassword"：  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   下列命令會將檔案系統中特定資料夾內所有封裝的 `ProtectionLevel` 屬性設為層級 2「機密資料以密碼加密」，並且將密碼設為 "strongpassword"：  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         如果您要對批次檔使用類似命令，請將檔案預留位置 "%f" 改輸入為批次檔適用的 "%%f"。  
  
## <a name="see-also"></a>另請參閱  
 [dtutil 公用程式](dtutil-utility.md)  
  
  
