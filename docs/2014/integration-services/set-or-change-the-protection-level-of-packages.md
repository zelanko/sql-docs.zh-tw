---
title: 設定或變更封裝的保護層級 |Microsoft Docs
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ee8ee5b2113d6fda6aaac72b407c899a610960bd
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66055846"
---
# <a name="set-or-change-the-protection-level-of-packages"></a>設定或變更封裝的保護等級
  若要控制封裝內容以及其中包含之機密值 (例如密碼) 的存取權，請設定 `ProtectionLevel` 屬性的值 包含在專案中的封裝需要有和專案相同的保護層級，才能建立專案。 如果您變更專案上的 `ProtectionLevel` 屬性設定，就需要手動更新封裝的屬性設定。  
  
 如需如何判斷`ProtectionLevel`中的設定適用於您的套件不同階段封裝生命週期中，請參閱[套件中敏感性資料的存取控制](security/access-control-for-sensitive-data-in-packages.md)。 如需 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 安全性功能的概觀，請參閱[安全性概觀 &#40;Integration Services&#41;](security/security-overview-integration-services.md)。  
  
 本主題中的程序說明如何使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 或 dtutil 命令提示字元公用程式來變更 `ProtectionLevel` 屬性。  
  
> [!NOTE]  
>  除了本主題中的程序之外，您通常可以在匯入或匯出封裝時，設定或變更封裝的 `ProtectionLevel` 屬性。 您也可以在使用 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 匯入和匯出精靈] 來儲存封裝時，變更封裝的 `ProtectionLevel` 屬性。  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>若要在 SQL Server 資料工具中設定或變更封裝的保護等級  
  
1.  檢閱可用的值`ProtectionLevel`主題中的屬性[設定封裝的保護層級](security/access-control-for-sensitive-data-in-packages.md)，並決定適當的值，為您的封裝。  
  
2.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計器中，開啟封裝。  
  
4.  如果 [屬性] 視窗並未顯示封裝屬性，請按一下設計介面。  
  
5.  在 [屬性] 視窗中，在**安全性**群組中，選取適當的值`ProtectionLevel`屬性。  
  
     如果您選取了需要密碼的保護等級，請輸入密碼作為 **PackagePassword** 屬性的值。  
  
6.  在 [檔案] 功能表上，選取 [儲存選取項目] 以儲存修改過的封裝。  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>在命令提示字元設定或變更封裝的保護等級  
  
1.  檢閱可用的值`ProtectionLevel`主題中的屬性[設定封裝的保護層級](security/access-control-for-sensitive-data-in-packages.md)，並決定適當的值，為您的封裝。  
  
2.  檢閱的對應`Encrypt`主題中的選項[dtutil Utility](dtutil-utility.md)，並決定適當的整數，用做為所選的值`ProtectionLevel`屬性。  
  
3.  開啟 [命令提示字元] 視窗。  
  
4.  在命令提示字元，導覽至您要設定其 `ProtectionLevel` 屬性之封裝的所在資料夾。  
  
     下列步驟所示的語法範例假設此資料夾為目前的資料夾。  
  
5.  使用類似於下列其中一個範例的命令，設定或變更封裝的保護等級：  
  
    -   下列命令會將檔案系統中個別封裝的 `ProtectionLevel` 屬性設為層級 2「機密資料以密碼加密」，並且將密碼設為 "strongpassword"：  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   下列命令會將檔案系統中特定資料夾內所有封裝的 `ProtectionLevel` 屬性設為層級 2「機密資料以密碼加密」，並且將密碼設為 "strongpassword"：  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         如果您要對批次檔使用類似命令，請將檔案預留位置 "%f" 改輸入為批次檔適用的 "%%f"。  
  
## <a name="see-also"></a>另請參閱  
 [Encrypt](dtutil-utility.md)  
  
  
